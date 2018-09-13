---
title: Troubleshooting Azure Active Directory B2B collaboration | Microsoft Docs
description: Remedies for common problems with Azure Active Directory B2B collaboration
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 05/25/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: a3b5b7150ddb1dcf0715d9c0726353eaf17626f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857851"
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="e469e-103">Troubleshooting Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="e469e-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="e469e-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span><span class="sxs-lookup"><span data-stu-id="e469e-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="e469e-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span><span class="sxs-lookup"><span data-stu-id="e469e-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="e469e-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span><span class="sxs-lookup"><span data-stu-id="e469e-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="e469e-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span><span class="sxs-lookup"><span data-stu-id="e469e-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="e469e-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span><span class="sxs-lookup"><span data-stu-id="e469e-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="e469e-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span><span class="sxs-lookup"><span data-stu-id="e469e-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="e469e-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span><span class="sxs-lookup"><span data-stu-id="e469e-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="e469e-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span><span class="sxs-lookup"><span data-stu-id="e469e-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="e469e-112">Invitations have been disabled for directory</span><span class="sxs-lookup"><span data-stu-id="e469e-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="e469e-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span><span class="sxs-lookup"><span data-stu-id="e469e-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/troubleshoot/external-user-settings.png)

<span data-ttu-id="e469e-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span><span class="sxs-lookup"><span data-stu-id="e469e-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="e469e-115">The user that I invited is receiving an error during redemption</span><span class="sxs-lookup"><span data-stu-id="e469e-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="e469e-116">Common errors include:</span><span class="sxs-lookup"><span data-stu-id="e469e-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="e469e-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span><span class="sxs-lookup"><span data-stu-id="e469e-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="e469e-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="e469e-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="e469e-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span><span class="sxs-lookup"><span data-stu-id="e469e-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="e469e-120">The user must check with their admin to determine if external users are allowed.</span><span class="sxs-lookup"><span data-stu-id="e469e-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="e469e-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span><span class="sxs-lookup"><span data-stu-id="e469e-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/troubleshoot/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="e469e-122">External user does not exist already in a federated domain</span><span class="sxs-lookup"><span data-stu-id="e469e-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="e469e-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span><span class="sxs-lookup"><span data-stu-id="e469e-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="e469e-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e469e-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="e469e-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e469e-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="e469e-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT#@fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e469e-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT#@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="e469e-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e469e-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="e469e-128">I receive an error when adding external users to a synchronized group</span><span class="sxs-lookup"><span data-stu-id="e469e-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="e469e-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span><span class="sxs-lookup"><span data-stu-id="e469e-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="e469e-130">My external user did not receive an email to redeem</span><span class="sxs-lookup"><span data-stu-id="e469e-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="e469e-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="e469e-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="e469e-132">I notice that the custom message does not get included with invitation messages at times</span><span class="sxs-lookup"><span data-stu-id="e469e-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="e469e-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span><span class="sxs-lookup"><span data-stu-id="e469e-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="e469e-134">The inviter doesn’t have an email address in the inviting tenant</span><span class="sxs-lookup"><span data-stu-id="e469e-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="e469e-135">When an appservice principal sends the invitation</span><span class="sxs-lookup"><span data-stu-id="e469e-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="e469e-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span><span class="sxs-lookup"><span data-stu-id="e469e-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="e469e-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span><span class="sxs-lookup"><span data-stu-id="e469e-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e469e-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="e469e-138">Next steps</span></span>

- [<span data-ttu-id="e469e-139">Get support for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="e469e-139">Get support for B2B collaboration</span></span>](get-support.md)