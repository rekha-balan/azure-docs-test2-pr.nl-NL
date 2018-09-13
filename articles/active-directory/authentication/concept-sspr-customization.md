---
title: Customizing Azure AD self-service password reset
description: Customization options for Azure AD self-service password reset
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 69f6ed7814feacbd5adf60325aae123d388ffb61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856326"
---
# <a name="customize-the-azure-ad-functionality-for-self-service-password-reset"></a><span data-ttu-id="35faa-103">Customize the Azure AD functionality for self-service password reset</span><span class="sxs-lookup"><span data-stu-id="35faa-103">Customize the Azure AD functionality for self-service password reset</span></span>

<span data-ttu-id="35faa-104">IT professionals who want to deploy self-service password reset (SSPR) in Azure Active directory (Azure AD) can customize the experience to match their users' needs.</span><span class="sxs-lookup"><span data-stu-id="35faa-104">IT professionals who want to deploy self-service password reset (SSPR) in Azure Active directory (Azure AD) can customize the experience to match their users' needs.</span></span>

## <a name="customize-the-contact-your-administrator-link"></a><span data-ttu-id="35faa-105">Customize the "Contact your administrator" link</span><span class="sxs-lookup"><span data-stu-id="35faa-105">Customize the "Contact your administrator" link</span></span>

<span data-ttu-id="35faa-106">Even if SSPR is not enabled, users still have a "Contact your administrator" link on the password reset portal.</span><span class="sxs-lookup"><span data-stu-id="35faa-106">Even if SSPR is not enabled, users still have a "Contact your administrator" link on the password reset portal.</span></span> <span data-ttu-id="35faa-107">If a user selects this link, it either:</span><span class="sxs-lookup"><span data-stu-id="35faa-107">If a user selects this link, it either:</span></span>

   * <span data-ttu-id="35faa-108">Emails your administrators and asks them for assistance in changing the user's password.</span><span class="sxs-lookup"><span data-stu-id="35faa-108">Emails your administrators and asks them for assistance in changing the user's password.</span></span>
   * <span data-ttu-id="35faa-109">Sends your users to a URL that you specify for assistance.</span><span class="sxs-lookup"><span data-stu-id="35faa-109">Sends your users to a URL that you specify for assistance.</span></span>

<span data-ttu-id="35faa-110">We recommend that you set this contact to something like an email address or website that your users already use for support questions.</span><span class="sxs-lookup"><span data-stu-id="35faa-110">We recommend that you set this contact to something like an email address or website that your users already use for support questions.</span></span>

<span data-ttu-id="35faa-111">![Contact][Contact]</span><span class="sxs-lookup"><span data-stu-id="35faa-111">![Contact][Contact]</span></span>

<span data-ttu-id="35faa-112">The contact email is sent to the following recipients in the following order:</span><span class="sxs-lookup"><span data-stu-id="35faa-112">The contact email is sent to the following recipients in the following order:</span></span>

1. <span data-ttu-id="35faa-113">If the **password administrator** role is assigned, administrators with this role are notified.</span><span class="sxs-lookup"><span data-stu-id="35faa-113">If the **password administrator** role is assigned, administrators with this role are notified.</span></span>
2. <span data-ttu-id="35faa-114">If no password administrators are assigned, then administrators with the **user administrator** role are notified.</span><span class="sxs-lookup"><span data-stu-id="35faa-114">If no password administrators are assigned, then administrators with the **user administrator** role are notified.</span></span>
3. <span data-ttu-id="35faa-115">If neither of the previous roles are assigned, then the **global administrators** are notified.</span><span class="sxs-lookup"><span data-stu-id="35faa-115">If neither of the previous roles are assigned, then the **global administrators** are notified.</span></span>

<span data-ttu-id="35faa-116">In all cases, a maximum of 100 recipients are notified.</span><span class="sxs-lookup"><span data-stu-id="35faa-116">In all cases, a maximum of 100 recipients are notified.</span></span>

<span data-ttu-id="35faa-117">To find out more about the different administrator roles and how to assign them, see [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="35faa-117">To find out more about the different administrator roles and how to assign them, see [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md).</span></span>

### <a name="disable-contact-your-administrator-emails"></a><span data-ttu-id="35faa-118">Disable "Contact your administrator" emails</span><span class="sxs-lookup"><span data-stu-id="35faa-118">Disable "Contact your administrator" emails</span></span>

<span data-ttu-id="35faa-119">If your organization does not want to notify administrators about password reset requests, you can enable the following configuration:</span><span class="sxs-lookup"><span data-stu-id="35faa-119">If your organization does not want to notify administrators about password reset requests, you can enable the following configuration:</span></span>

* <span data-ttu-id="35faa-120">Enable self-service password reset for all end users.</span><span class="sxs-lookup"><span data-stu-id="35faa-120">Enable self-service password reset for all end users.</span></span> <span data-ttu-id="35faa-121">This option is under **Password Reset** > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="35faa-121">This option is under **Password Reset** > **Properties**.</span></span> <span data-ttu-id="35faa-122">If you don't want users to reset their own passwords, you can scope access to an empty group.</span><span class="sxs-lookup"><span data-stu-id="35faa-122">If you don't want users to reset their own passwords, you can scope access to an empty group.</span></span> <span data-ttu-id="35faa-123">*We don't recommend this option.*</span><span class="sxs-lookup"><span data-stu-id="35faa-123">*We don't recommend this option.*</span></span>
* <span data-ttu-id="35faa-124">Customize the helpdesk link to provide a web URL or mailto: address that users can use to get assistance.</span><span class="sxs-lookup"><span data-stu-id="35faa-124">Customize the helpdesk link to provide a web URL or mailto: address that users can use to get assistance.</span></span> <span data-ttu-id="35faa-125">This option is under **Password Reset** > **Customization** > **Custom helpdesk email or URL**.</span><span class="sxs-lookup"><span data-stu-id="35faa-125">This option is under **Password Reset** > **Customization** > **Custom helpdesk email or URL**.</span></span>

## <a name="customize-the-ad-fs-sign-in-page-for-sspr"></a><span data-ttu-id="35faa-126">Customize the AD FS sign-in page for SSPR</span><span class="sxs-lookup"><span data-stu-id="35faa-126">Customize the AD FS sign-in page for SSPR</span></span>

<span data-ttu-id="35faa-127">Active Directory Federation Services (AD FS) administrators can add a link to their sign-in page by using the guidance found in the [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description) article.</span><span class="sxs-lookup"><span data-stu-id="35faa-127">Active Directory Federation Services (AD FS) administrators can add a link to their sign-in page by using the guidance found in the [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description) article.</span></span>

<span data-ttu-id="35faa-128">To add a link to the AD FS sign-in page, use the following command on your AD FS server.</span><span class="sxs-lookup"><span data-stu-id="35faa-128">To add a link to the AD FS sign-in page, use the following command on your AD FS server.</span></span> <span data-ttu-id="35faa-129">Users can use this page to enter the SSPR workflow.</span><span class="sxs-lookup"><span data-stu-id="35faa-129">Users can use this page to enter the SSPR workflow.</span></span>

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href='https://passwordreset.microsoftonline.com' target='_blank'>Can’t access your account?</A></p>" ```

## <a name="customize-the-sign-in-page-and-access-panel-look-and-feel"></a><span data-ttu-id="35faa-130">Customize the sign-in page and access panel look and feel</span><span class="sxs-lookup"><span data-stu-id="35faa-130">Customize the sign-in page and access panel look and feel</span></span>

<span data-ttu-id="35faa-131">You can customize the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="35faa-131">You can customize the sign-in page.</span></span> <span data-ttu-id="35faa-132">You can add a logo that appears along with the image that fits your company branding.</span><span class="sxs-lookup"><span data-stu-id="35faa-132">You can add a logo that appears along with the image that fits your company branding.</span></span>

<span data-ttu-id="35faa-133">The graphics you choose are shown in the following circumstances:</span><span class="sxs-lookup"><span data-stu-id="35faa-133">The graphics you choose are shown in the following circumstances:</span></span>

* <span data-ttu-id="35faa-134">After a user enters their username</span><span class="sxs-lookup"><span data-stu-id="35faa-134">After a user enters their username</span></span>
* <span data-ttu-id="35faa-135">If the user accesses the customized URL:</span><span class="sxs-lookup"><span data-stu-id="35faa-135">If the user accesses the customized URL:</span></span>
    * <span data-ttu-id="35faa-136">By passing the *whr* parameter to the password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span><span class="sxs-lookup"><span data-stu-id="35faa-136">By passing the *whr* parameter to the password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span></span>
    * <span data-ttu-id="35faa-137">By passing the *username* parameter to the password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="35faa-137">By passing the *username* parameter to the password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span></span>

<span data-ttu-id="35faa-138">Find details on how to configure company branding in the article [Add company branding to your sign-in page in Azure AD](../fundamentals/customize-branding.md).</span><span class="sxs-lookup"><span data-stu-id="35faa-138">Find details on how to configure company branding in the article [Add company branding to your sign-in page in Azure AD](../fundamentals/customize-branding.md).</span></span>

### <a name="directory-name"></a><span data-ttu-id="35faa-139">Directory name</span><span class="sxs-lookup"><span data-stu-id="35faa-139">Directory name</span></span>

<span data-ttu-id="35faa-140">You can change the directory name attribute under **Azure Active Directory** > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="35faa-140">You can change the directory name attribute under **Azure Active Directory** > **Properties**.</span></span> <span data-ttu-id="35faa-141">You can show a friendly organization name that is seen in the portal and in the automated communications.</span><span class="sxs-lookup"><span data-stu-id="35faa-141">You can show a friendly organization name that is seen in the portal and in the automated communications.</span></span> <span data-ttu-id="35faa-142">This option is the most visible in automated emails in the forms that follow:</span><span class="sxs-lookup"><span data-stu-id="35faa-142">This option is the most visible in automated emails in the forms that follow:</span></span>

* <span data-ttu-id="35faa-143">The friendly name in the email, for example “Microsoft on behalf of CONTOSO demo”</span><span class="sxs-lookup"><span data-stu-id="35faa-143">The friendly name in the email, for example “Microsoft on behalf of CONTOSO demo”</span></span>
* <span data-ttu-id="35faa-144">The subject line in the email, for example “CONTOSO demo account email verification code”</span><span class="sxs-lookup"><span data-stu-id="35faa-144">The subject line in the email, for example “CONTOSO demo account email verification code”</span></span>

## <a name="next-steps"></a><span data-ttu-id="35faa-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="35faa-145">Next steps</span></span>

* [<span data-ttu-id="35faa-146">How do I complete a successful rollout of SSPR?</span><span class="sxs-lookup"><span data-stu-id="35faa-146">How do I complete a successful rollout of SSPR?</span></span>](howto-sspr-deployment.md)
* [<span data-ttu-id="35faa-147">Reset or change your password</span><span class="sxs-lookup"><span data-stu-id="35faa-147">Reset or change your password</span></span>](../user-help/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="35faa-148">Register for self-service password reset</span><span class="sxs-lookup"><span data-stu-id="35faa-148">Register for self-service password reset</span></span>](../user-help/active-directory-passwords-reset-register.md)
* [<span data-ttu-id="35faa-149">Do you have a licensing question?</span><span class="sxs-lookup"><span data-stu-id="35faa-149">Do you have a licensing question?</span></span>](concept-sspr-licensing.md)
* [<span data-ttu-id="35faa-150">What data is used by SSPR and what data should you populate for your users?</span><span class="sxs-lookup"><span data-stu-id="35faa-150">What data is used by SSPR and what data should you populate for your users?</span></span>](howto-sspr-authenticationdata.md)
* [<span data-ttu-id="35faa-151">What authentication methods are available to users?</span><span class="sxs-lookup"><span data-stu-id="35faa-151">What authentication methods are available to users?</span></span>](concept-sspr-howitworks.md#authentication-methods)
* [<span data-ttu-id="35faa-152">What are the policy options with SSPR?</span><span class="sxs-lookup"><span data-stu-id="35faa-152">What are the policy options with SSPR?</span></span>](concept-sspr-policy.md)
* [<span data-ttu-id="35faa-153">What is password writeback and why do I care about it?</span><span class="sxs-lookup"><span data-stu-id="35faa-153">What is password writeback and why do I care about it?</span></span>](howto-sspr-writeback.md)
* [<span data-ttu-id="35faa-154">How do I report on activity in SSPR?</span><span class="sxs-lookup"><span data-stu-id="35faa-154">How do I report on activity in SSPR?</span></span>](howto-sspr-reporting.md)
* [<span data-ttu-id="35faa-155">What are all of the options in SSPR and what do they mean?</span><span class="sxs-lookup"><span data-stu-id="35faa-155">What are all of the options in SSPR and what do they mean?</span></span>](concept-sspr-howitworks.md)
* [<span data-ttu-id="35faa-156">I think something is broken. How do I troubleshoot SSPR?</span><span class="sxs-lookup"><span data-stu-id="35faa-156">I think something is broken. How do I troubleshoot SSPR?</span></span>](active-directory-passwords-troubleshoot.md)
* [<span data-ttu-id="35faa-157">I have a question that was not covered somewhere else</span><span class="sxs-lookup"><span data-stu-id="35faa-157">I have a question that was not covered somewhere else</span></span>](active-directory-passwords-faq.md)

[Contact]: ./media/concept-sspr-customization/sspr-contact-admin.png "Contact your administrator for help resetting your password email example"
