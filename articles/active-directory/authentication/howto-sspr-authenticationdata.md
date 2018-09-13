---
title: Azure AD SSPR data requirements | Microsoft Docs
description: Data requirements for Azure AD self-service password reset and how to satisfy them
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 5d8fe6282d956d7f399aff9f7aa250c5061dc887
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868341"
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="9b7bf-103">Deploy password reset without requiring end-user registration</span><span class="sxs-lookup"><span data-stu-id="9b7bf-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="9b7bf-104">To deploy Azure Active Directory (Azure AD) self-service password reset (SSPR), authentication data needs to be present.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-104">To deploy Azure Active Directory (Azure AD) self-service password reset (SSPR), authentication data needs to be present.</span></span> <span data-ttu-id="9b7bf-105">Some organizations have their users enter their authentication data themselves.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-105">Some organizations have their users enter their authentication data themselves.</span></span> <span data-ttu-id="9b7bf-106">But many organizations prefer to synchronize with data that already exists in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-106">But many organizations prefer to synchronize with data that already exists in Active Directory.</span></span> <span data-ttu-id="9b7bf-107">The synced data is made available to Azure AD and SSPR without requiring user interaction if you:</span><span class="sxs-lookup"><span data-stu-id="9b7bf-107">The synced data is made available to Azure AD and SSPR without requiring user interaction if you:</span></span>
   * <span data-ttu-id="9b7bf-108">Properly format the data in your on-premises directory.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-108">Properly format the data in your on-premises directory.</span></span>
   * <span data-ttu-id="9b7bf-109">Configure [Azure AD Connect by using the express settings](./../connect/active-directory-aadconnect-get-started-express.md).</span><span class="sxs-lookup"><span data-stu-id="9b7bf-109">Configure [Azure AD Connect by using the express settings](./../connect/active-directory-aadconnect-get-started-express.md).</span></span>

<span data-ttu-id="9b7bf-110">To work properly, phone numbers must be in the format *+CountryCode PhoneNumber*, for example, +1 4255551234.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-110">To work properly, phone numbers must be in the format *+CountryCode PhoneNumber*, for example, +1 4255551234.</span></span>

> [!NOTE]
> <span data-ttu-id="9b7bf-111">There needs to be a space between the country code and the phone number.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-111">There needs to be a space between the country code and the phone number.</span></span>
>
> <span data-ttu-id="9b7bf-112">Password reset does not support phone extensions.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-112">Password reset does not support phone extensions.</span></span> <span data-ttu-id="9b7bf-113">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-113">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="9b7bf-114">Fields populated</span><span class="sxs-lookup"><span data-stu-id="9b7bf-114">Fields populated</span></span>

<span data-ttu-id="9b7bf-115">If you use the default settings in Azure AD Connect, the following mappings are made:</span><span class="sxs-lookup"><span data-stu-id="9b7bf-115">If you use the default settings in Azure AD Connect, the following mappings are made:</span></span>

| <span data-ttu-id="9b7bf-116">On-premises Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b7bf-116">On-premises Active Directory</span></span> | <span data-ttu-id="9b7bf-117">Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b7bf-117">Azure AD</span></span> |
| --- | --- |
| <span data-ttu-id="9b7bf-118">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="9b7bf-118">telephoneNumber</span></span> | <span data-ttu-id="9b7bf-119">Office phone</span><span class="sxs-lookup"><span data-stu-id="9b7bf-119">Office phone</span></span> |
| <span data-ttu-id="9b7bf-120">mobile</span><span class="sxs-lookup"><span data-stu-id="9b7bf-120">mobile</span></span> | <span data-ttu-id="9b7bf-121">Mobile phone</span><span class="sxs-lookup"><span data-stu-id="9b7bf-121">Mobile phone</span></span> |

<span data-ttu-id="9b7bf-122">Once a user verifies their mobile phone number, the Phone field under Authentication contact info in Azure AD will also be populated with that number.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-122">Once a user verifies their mobile phone number, the Phone field under Authentication contact info in Azure AD will also be populated with that number.</span></span>

## <a name="authentication-contact-info"></a><span data-ttu-id="9b7bf-123">Authentication contact info</span><span class="sxs-lookup"><span data-stu-id="9b7bf-123">Authentication contact info</span></span>

<span data-ttu-id="9b7bf-124">A Global Administrator can manually set the Authentication contact info for a user as displayed in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-124">A Global Administrator can manually set the Authentication contact info for a user as displayed in the following screenshot.</span></span>

<span data-ttu-id="9b7bf-125">![Contact][Contact]</span><span class="sxs-lookup"><span data-stu-id="9b7bf-125">![Contact][Contact]</span></span>

<span data-ttu-id="9b7bf-126">If the Phone field is populated and Mobile phone is enabled in the SSPR policy, the user will see that number on the password reset registration page and during the password reset workflow.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-126">If the Phone field is populated and Mobile phone is enabled in the SSPR policy, the user will see that number on the password reset registration page and during the password reset workflow.</span></span>

<span data-ttu-id="9b7bf-127">The Alternate phone field is not used for password reset.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-127">The Alternate phone field is not used for password reset.</span></span>

<span data-ttu-id="9b7bf-128">If the Email field is populated and Email is enabled in the SSPR policy, the user will see that email on the password reset registration page and during the password reset workflow.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-128">If the Email field is populated and Email is enabled in the SSPR policy, the user will see that email on the password reset registration page and during the password reset workflow.</span></span>

<span data-ttu-id="9b7bf-129">If the Alternate email field is populated and Email is enabled in the SSPR policy, the user will **not** see that email on the password reset registration page, but they will see it during the password reset workflow.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-129">If the Alternate email field is populated and Email is enabled in the SSPR policy, the user will **not** see that email on the password reset registration page, but they will see it during the password reset workflow.</span></span>

## <a name="security-questions-and-answers"></a><span data-ttu-id="9b7bf-130">Security questions and answers</span><span class="sxs-lookup"><span data-stu-id="9b7bf-130">Security questions and answers</span></span>

<span data-ttu-id="9b7bf-131">The security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="9b7bf-131">The security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="9b7bf-132">Administrators can't see, set, or modify the contents of another users' questions and answers.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-132">Administrators can't see, set, or modify the contents of another users' questions and answers.</span></span>

## <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="9b7bf-133">What happens when a user registers</span><span class="sxs-lookup"><span data-stu-id="9b7bf-133">What happens when a user registers</span></span>

<span data-ttu-id="9b7bf-134">When a user registers, the registration page sets the following fields:</span><span class="sxs-lookup"><span data-stu-id="9b7bf-134">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="9b7bf-135">**Authentication Phone**</span><span class="sxs-lookup"><span data-stu-id="9b7bf-135">**Authentication Phone**</span></span>
* <span data-ttu-id="9b7bf-136">**Authentication Email**</span><span class="sxs-lookup"><span data-stu-id="9b7bf-136">**Authentication Email**</span></span>
* <span data-ttu-id="9b7bf-137">**Security Questions and Answers**</span><span class="sxs-lookup"><span data-stu-id="9b7bf-137">**Security Questions and Answers**</span></span>

<span data-ttu-id="9b7bf-138">If you have provided a value for **Mobile phone** or **Alternate email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-138">If you have provided a value for **Mobile phone** or **Alternate email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="9b7bf-139">In addition, users see those values when they register for the first time, and they can modify them if they want to.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-139">In addition, users see those values when they register for the first time, and they can modify them if they want to.</span></span> <span data-ttu-id="9b7bf-140">After they register successfully, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-140">After they register successfully, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-the-authentication-data-through-powershell"></a><span data-ttu-id="9b7bf-141">Set and read the authentication data through PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b7bf-141">Set and read the authentication data through PowerShell</span></span>

<span data-ttu-id="9b7bf-142">The following fields can be set through PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b7bf-142">The following fields can be set through PowerShell:</span></span>

* <span data-ttu-id="9b7bf-143">**Alternate email**</span><span class="sxs-lookup"><span data-stu-id="9b7bf-143">**Alternate email**</span></span>
* <span data-ttu-id="9b7bf-144">**Mobile phone**</span><span class="sxs-lookup"><span data-stu-id="9b7bf-144">**Mobile phone**</span></span>
* <span data-ttu-id="9b7bf-145">**Office phone**: Can only be set if you're not synchronizing with an on-premises directory</span><span class="sxs-lookup"><span data-stu-id="9b7bf-145">**Office phone**: Can only be set if you're not synchronizing with an on-premises directory</span></span>

### <a name="use-powershell-version-1"></a><span data-ttu-id="9b7bf-146">Use PowerShell version 1</span><span class="sxs-lookup"><span data-stu-id="9b7bf-146">Use PowerShell version 1</span></span>

<span data-ttu-id="9b7bf-147">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="9b7bf-147">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="9b7bf-148">After you have it installed, you can use the steps that follow to configure each field.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-148">After you have it installed, you can use the steps that follow to configure each field.</span></span>

#### <a name="set-the-authentication-data-with-powershell-version-1"></a><span data-ttu-id="9b7bf-149">Set the authentication data with PowerShell version 1</span><span class="sxs-lookup"><span data-stu-id="9b7bf-149">Set the authentication data with PowerShell version 1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-the-authentication-data-with-powershell-version-1"></a><span data-ttu-id="9b7bf-150">Read the authentication data with PowerShell version 1</span><span class="sxs-lookup"><span data-stu-id="9b7bf-150">Read the authentication data with PowerShell version 1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="read-the-authentication-phone-and-authentication-email-options"></a><span data-ttu-id="9b7bf-151">Read the Authentication Phone and Authentication Email options</span><span class="sxs-lookup"><span data-stu-id="9b7bf-151">Read the Authentication Phone and Authentication Email options</span></span>

<span data-ttu-id="9b7bf-152">To read the **Authentication Phone** and **Authentication Email** when you use PowerShell version 1, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="9b7bf-152">To read the **Authentication Phone** and **Authentication Email** when you use PowerShell version 1, use the following commands:</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="use-powershell-version-2"></a><span data-ttu-id="9b7bf-153">Use PowerShell version 2</span><span class="sxs-lookup"><span data-stu-id="9b7bf-153">Use PowerShell version 2</span></span>

<span data-ttu-id="9b7bf-154">To get started, you need to [download and install the Azure AD version 2 PowerShell module](https://docs.microsoft.com/powershell/module/azuread/?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="9b7bf-154">To get started, you need to [download and install the Azure AD version 2 PowerShell module](https://docs.microsoft.com/powershell/module/azuread/?view=azureadps-2.0).</span></span> <span data-ttu-id="9b7bf-155">After you have it installed, you can use the steps that follow to configure each field.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-155">After you have it installed, you can use the steps that follow to configure each field.</span></span>

<span data-ttu-id="9b7bf-156">To quickly install from recent versions of PowerShell that support Install-Module, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="9b7bf-156">To quickly install from recent versions of PowerShell that support Install-Module, run the following commands.</span></span> <span data-ttu-id="9b7bf-157">(The first line checks to see if the module is already installed.)</span><span class="sxs-lookup"><span data-stu-id="9b7bf-157">(The first line checks to see if the module is already installed.)</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-the-authentication-data-with-powershell-version-2"></a><span data-ttu-id="9b7bf-158">Set the authentication data with PowerShell version 2</span><span class="sxs-lookup"><span data-stu-id="9b7bf-158">Set the authentication data with PowerShell version 2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

#### <a name="read-the-authentication-data-with-powershell-version-2"></a><span data-ttu-id="9b7bf-159">Read the authentication data with PowerShell version 2</span><span class="sxs-lookup"><span data-stu-id="9b7bf-159">Read the authentication data with PowerShell version 2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="9b7bf-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b7bf-160">Next steps</span></span>

* [<span data-ttu-id="9b7bf-161">How do I complete a successful rollout of SSPR?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-161">How do I complete a successful rollout of SSPR?</span></span>](howto-sspr-deployment.md)
* [<span data-ttu-id="9b7bf-162">Reset or change your password</span><span class="sxs-lookup"><span data-stu-id="9b7bf-162">Reset or change your password</span></span>](../user-help/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="9b7bf-163">Register for self-service password reset</span><span class="sxs-lookup"><span data-stu-id="9b7bf-163">Register for self-service password reset</span></span>](../user-help/active-directory-passwords-reset-register.md)
* [<span data-ttu-id="9b7bf-164">Do you have a licensing question?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-164">Do you have a licensing question?</span></span>](concept-sspr-licensing.md)
* [<span data-ttu-id="9b7bf-165">What authentication methods are available to users?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-165">What authentication methods are available to users?</span></span>](concept-sspr-howitworks.md#authentication-methods)
* [<span data-ttu-id="9b7bf-166">What are the policy options with SSPR?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-166">What are the policy options with SSPR?</span></span>](concept-sspr-policy.md)
* [<span data-ttu-id="9b7bf-167">What is password writeback and why do I care about it?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-167">What is password writeback and why do I care about it?</span></span>](howto-sspr-writeback.md)
* [<span data-ttu-id="9b7bf-168">How do I report on activity in SSPR?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-168">How do I report on activity in SSPR?</span></span>](howto-sspr-reporting.md)
* [<span data-ttu-id="9b7bf-169">What are all of the options in SSPR and what do they mean?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-169">What are all of the options in SSPR and what do they mean?</span></span>](concept-sspr-howitworks.md)
* [<span data-ttu-id="9b7bf-170">I think something is broken. How do I troubleshoot SSPR?</span><span class="sxs-lookup"><span data-stu-id="9b7bf-170">I think something is broken. How do I troubleshoot SSPR?</span></span>](active-directory-passwords-troubleshoot.md)
* [<span data-ttu-id="9b7bf-171">I have a question that was not covered somewhere else</span><span class="sxs-lookup"><span data-stu-id="9b7bf-171">I have a question that was not covered somewhere else</span></span>](active-directory-passwords-faq.md)

[Contact]: ./media/howto-sspr-authenticationdata/user-authentication-contact-info.png "Global administrators can modify a user's authentication contact info"
