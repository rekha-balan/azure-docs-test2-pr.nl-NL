---
title: Troubleshooting Azure Active Directory B2B collaboration | Microsoft Docs
description: Remedies for common problems with Azure Active Directory B2B collaboration
services: active-directory
documentationcenter: ''
author: sasubram
manager: femila
editor: ''
tags: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: 6f37dc20fc2e68f1bf7c5a65cb712b2a5241042d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551967"
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="9b75f-103">Troubleshooting Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="9b75f-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="9b75f-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span><span class="sxs-lookup"><span data-stu-id="9b75f-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="9b75f-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span><span class="sxs-lookup"><span data-stu-id="9b75f-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="9b75f-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span><span class="sxs-lookup"><span data-stu-id="9b75f-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="9b75f-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span><span class="sxs-lookup"><span data-stu-id="9b75f-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="9b75f-108">The ability to search for existing guest users in the SharePoint Online people picker is OFF by default to match legacy behavior.</span><span class="sxs-lookup"><span data-stu-id="9b75f-108">The ability to search for existing guest users in the SharePoint Online people picker is OFF by default to match legacy behavior.</span></span>
<span data-ttu-id="9b75f-109">You can enable this using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span><span class="sxs-lookup"><span data-stu-id="9b75f-109">You can enable this using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="9b75f-110">This can be set using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span><span class="sxs-lookup"><span data-stu-id="9b75f-110">This can be set using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="9b75f-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span><span class="sxs-lookup"><span data-stu-id="9b75f-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="9b75f-112">Invitations have been disabled for directory</span><span class="sxs-lookup"><span data-stu-id="9b75f-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="9b75f-113">If you receive an error message indicating that you do not have permissions to invite users, verify that your user account is authorized to invite external users.</span><span class="sxs-lookup"><span data-stu-id="9b75f-113">If you receive an error message indicating that you do not have permissions to invite users, verify that your user account is authorized to invite external users.</span></span> <span data-ttu-id="9b75f-114">This can be done under User Settings:</span><span class="sxs-lookup"><span data-stu-id="9b75f-114">This can be done under User Settings:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="9b75f-115">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span><span class="sxs-lookup"><span data-stu-id="9b75f-115">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="9b75f-116">The user that I invited is receiving an error during redemption</span><span class="sxs-lookup"><span data-stu-id="9b75f-116">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="9b75f-117">Common errors include:</span><span class="sxs-lookup"><span data-stu-id="9b75f-117">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="9b75f-118">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span><span class="sxs-lookup"><span data-stu-id="9b75f-118">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="9b75f-119">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="9b75f-119">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="9b75f-120">The administrator of contoso.com may have a policy in place preventing users from being created.</span><span class="sxs-lookup"><span data-stu-id="9b75f-120">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="9b75f-121">The user must check with their admin to determine if external users are allowed.</span><span class="sxs-lookup"><span data-stu-id="9b75f-121">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="9b75f-122">The external user’s admin may need to allow Email Verified users in their domain (see this [article](https://docs.microsoft.com/powershell/msonline/v1/set-msolcompanysettings#parameters) on allowing Email Verified Users).</span><span class="sxs-lookup"><span data-stu-id="9b75f-122">The external user’s admin may need to allow Email Verified users in their domain (see this [article](https://docs.microsoft.com/powershell/msonline/v1/set-msolcompanysettings#parameters) on allowing Email Verified Users).</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="9b75f-123">External user does not exist already in a federated domain</span><span class="sxs-lookup"><span data-stu-id="9b75f-123">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="9b75f-124">In cases where the external user is using a federation solution where authentication is being performed on-premises and the user does not already exist in Azure Active Directory, the user cannot be invited.</span><span class="sxs-lookup"><span data-stu-id="9b75f-124">In cases where the external user is using a federation solution where authentication is being performed on-premises and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="9b75f-125">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b75f-125">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="9b75f-126">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span><span class="sxs-lookup"><span data-stu-id="9b75f-126">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="9b75f-127">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users (that is, user@contoso.com invited, becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com) so \# in UPNs coming from on-premises are not allowed to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9b75f-127">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users (that is, user@contoso.com invited, becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com) so \# in UPNs coming from on-premises are not allowed to sign in to the Azure portal.</span></span>

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="9b75f-128">I receive an error when adding external users to a synchronized group</span><span class="sxs-lookup"><span data-stu-id="9b75f-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="9b75f-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span><span class="sxs-lookup"><span data-stu-id="9b75f-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="9b75f-130">My external user did not receive an email to redeem</span><span class="sxs-lookup"><span data-stu-id="9b75f-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="9b75f-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="9b75f-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="9b75f-132">I notice that the custom message does not get included with invitation messages at times</span><span class="sxs-lookup"><span data-stu-id="9b75f-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="9b75f-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when the inviter doesn’t have an email address in the resource organization (otherwise known as the inviting tenancy) or when an app service principal sends the invitation.</span><span class="sxs-lookup"><span data-stu-id="9b75f-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when the inviter doesn’t have an email address in the resource organization (otherwise known as the inviting tenancy) or when an app service principal sends the invitation.</span></span> <span data-ttu-id="9b75f-134">If this is an important scenario for you, you can suppress our API sending the invitation email and send it through an email mechanism of your choice.</span><span class="sxs-lookup"><span data-stu-id="9b75f-134">If this is an important scenario for you, you can suppress our API sending the invitation email and send it through an email mechanism of your choice.</span></span> <span data-ttu-id="9b75f-135">Remember to consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span><span class="sxs-lookup"><span data-stu-id="9b75f-135">Remember to consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b75f-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b75f-136">Next steps</span></span>

<span data-ttu-id="9b75f-137">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="9b75f-137">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="9b75f-138">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="9b75f-138">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="9b75f-139">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="9b75f-139">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="9b75f-140">How do information workers add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="9b75f-140">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="9b75f-141">The elements of the B2B collaboration invitation email</span><span class="sxs-lookup"><span data-stu-id="9b75f-141">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="9b75f-142">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="9b75f-142">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="9b75f-143">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="9b75f-143">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="9b75f-144">Azure Active Directory B2B collaboration frequently-asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="9b75f-144">Azure Active Directory B2B collaboration frequently-asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="9b75f-145">Azure Active Directory B2B collaboration API and customization</span><span class="sxs-lookup"><span data-stu-id="9b75f-145">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="9b75f-146">Multi-factor authentication for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="9b75f-146">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="9b75f-147">Add B2B collaboration users without an invitation</span><span class="sxs-lookup"><span data-stu-id="9b75f-147">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="9b75f-148">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b75f-148">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)


