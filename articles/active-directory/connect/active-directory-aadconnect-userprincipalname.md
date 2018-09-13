---
title: Azure AD UserPrincipalName population
description: The following document describes how the UserPrincipalName attribute is populated.
author: billmath
ms.component: hybrid
ms.author: billmath
ms.date: 06/26/2018
ms.topic: article
ms.workload: identity
ms.service: active-Directory
manager: mtillman
ms.openlocfilehash: 6b3fddcdf6ff9c35d5932b9b83da02f60f9e081e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866452"
---
# <a name="azure-ad-userprincipalname-population"></a><span data-ttu-id="c04c4-103">Azure AD UserPrincipalName population</span><span class="sxs-lookup"><span data-stu-id="c04c4-103">Azure AD UserPrincipalName population</span></span>

<span data-ttu-id="c04c4-104">This article describes how the UserPrincipalName attribute is populated in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c04c4-104">This article describes how the UserPrincipalName attribute is populated in Azure Active Directory (Azure AD).</span></span>
<span data-ttu-id="c04c4-105">The UserPrincipalName attribute value is the Azure AD username for the user accounts.</span><span class="sxs-lookup"><span data-stu-id="c04c4-105">The UserPrincipalName attribute value is the Azure AD username for the user accounts.</span></span>

## <a name="upn-terminology"></a><span data-ttu-id="c04c4-106">UPN terminology</span><span class="sxs-lookup"><span data-stu-id="c04c4-106">UPN terminology</span></span>
<span data-ttu-id="c04c4-107">The following terminology is used in this article:</span><span class="sxs-lookup"><span data-stu-id="c04c4-107">The following terminology is used in this article:</span></span>

|<span data-ttu-id="c04c4-108">Term</span><span class="sxs-lookup"><span data-stu-id="c04c4-108">Term</span></span>|<span data-ttu-id="c04c4-109">Description</span><span class="sxs-lookup"><span data-stu-id="c04c4-109">Description</span></span>|
|-----|-----|
|<span data-ttu-id="c04c4-110">Initial domain</span><span class="sxs-lookup"><span data-stu-id="c04c4-110">Initial domain</span></span>|<span data-ttu-id="c04c4-111">The default domain (onmicrosoft.com) in the Azure AD Tenant.</span><span class="sxs-lookup"><span data-stu-id="c04c4-111">The default domain (onmicrosoft.com) in the Azure AD Tenant.</span></span> <span data-ttu-id="c04c4-112">For example, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c04c4-112">For example, contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="c04c4-113">Microsoft Online Email Routing Address (MOERA)</span><span class="sxs-lookup"><span data-stu-id="c04c4-113">Microsoft Online Email Routing Address (MOERA)</span></span>|<span data-ttu-id="c04c4-114">Azure AD calculates the MOERA from Azure AD MailNickName attribute and Azure AD initial domain as &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span><span class="sxs-lookup"><span data-stu-id="c04c4-114">Azure AD calculates the MOERA from Azure AD MailNickName attribute and Azure AD initial domain as &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span></span>|
|<span data-ttu-id="c04c4-115">On-premises mailNickName attribute</span><span class="sxs-lookup"><span data-stu-id="c04c4-115">On-premises mailNickName attribute</span></span>|<span data-ttu-id="c04c4-116">An attribute in Active Directory, the value of which represents the alias of a user in an Exchange organization.</span><span class="sxs-lookup"><span data-stu-id="c04c4-116">An attribute in Active Directory, the value of which represents the alias of a user in an Exchange organization.</span></span>|
|<span data-ttu-id="c04c4-117">On-premises mail attribute</span><span class="sxs-lookup"><span data-stu-id="c04c4-117">On-premises mail attribute</span></span>|<span data-ttu-id="c04c4-118">An attribute in Active Directory, the value of which represents the email address of a user</span><span class="sxs-lookup"><span data-stu-id="c04c4-118">An attribute in Active Directory, the value of which represents the email address of a user</span></span>|
|<span data-ttu-id="c04c4-119">Primary SMTP Address</span><span class="sxs-lookup"><span data-stu-id="c04c4-119">Primary SMTP Address</span></span>|<span data-ttu-id="c04c4-120">The primary email address of an Exchange recipient object.</span><span class="sxs-lookup"><span data-stu-id="c04c4-120">The primary email address of an Exchange recipient object.</span></span> <span data-ttu-id="c04c4-121">For example, SMTP:user\@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c04c4-121">For example, SMTP:user\@contoso.com.</span></span>|
|<span data-ttu-id="c04c4-122">Alternate login ID</span><span class="sxs-lookup"><span data-stu-id="c04c4-122">Alternate login ID</span></span>|<span data-ttu-id="c04c4-123">An on-premises attribute other than UserPrincipalName, such as mail attribute, used for sign-in.</span><span class="sxs-lookup"><span data-stu-id="c04c4-123">An on-premises attribute other than UserPrincipalName, such as mail attribute, used for sign-in.</span></span>|

## <a name="what-is-userprincipalname"></a><span data-ttu-id="c04c4-124">What is UserPrincipalName?</span><span class="sxs-lookup"><span data-stu-id="c04c4-124">What is UserPrincipalName?</span></span>
<span data-ttu-id="c04c4-125">UserPrincipalName is an attribute that is an Internet-style login name for a user based on the Internet standard [RFC 822](http://www.ietf.org/rfc/rfc0822.txt).</span><span class="sxs-lookup"><span data-stu-id="c04c4-125">UserPrincipalName is an attribute that is an Internet-style login name for a user based on the Internet standard [RFC 822](http://www.ietf.org/rfc/rfc0822.txt).</span></span> 

### <a name="upn-format"></a><span data-ttu-id="c04c4-126">UPN format</span><span class="sxs-lookup"><span data-stu-id="c04c4-126">UPN format</span></span>
<span data-ttu-id="c04c4-127">A UPN consists of a UPN prefix (the user account name) and a UPN suffix (a DNS domain name).</span><span class="sxs-lookup"><span data-stu-id="c04c4-127">A UPN consists of a UPN prefix (the user account name) and a UPN suffix (a DNS domain name).</span></span> <span data-ttu-id="c04c4-128">The prefix is joined with the suffix using the "\@" symbol.</span><span class="sxs-lookup"><span data-stu-id="c04c4-128">The prefix is joined with the suffix using the "\@" symbol.</span></span> <span data-ttu-id="c04c4-129">For example, "someone\@example.com".</span><span class="sxs-lookup"><span data-stu-id="c04c4-129">For example, "someone\@example.com".</span></span> <span data-ttu-id="c04c4-130">A UPN must be unique among all security principal objects within a directory forest.</span><span class="sxs-lookup"><span data-stu-id="c04c4-130">A UPN must be unique among all security principal objects within a directory forest.</span></span> 

## <a name="upn-in-azure-ad"></a><span data-ttu-id="c04c4-131">UPN in Azure AD</span><span class="sxs-lookup"><span data-stu-id="c04c4-131">UPN in Azure AD</span></span> 
<span data-ttu-id="c04c4-132">The UPN is used by Azure AD to allow users to sign-in.</span><span class="sxs-lookup"><span data-stu-id="c04c4-132">The UPN is used by Azure AD to allow users to sign-in.</span></span>  <span data-ttu-id="c04c4-133">The UPN that a user can use, depends on whether or not the domain has been verified.</span><span class="sxs-lookup"><span data-stu-id="c04c4-133">The UPN that a user can use, depends on whether or not the domain has been verified.</span></span>  <span data-ttu-id="c04c4-134">If the domain has been verified, then a user with that suffix will be allowed to sign-in to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c04c4-134">If the domain has been verified, then a user with that suffix will be allowed to sign-in to Azure AD.</span></span>  

<span data-ttu-id="c04c4-135">The attribute is synchronized by Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c04c4-135">The attribute is synchronized by Azure AD Connect.</span></span>  <span data-ttu-id="c04c4-136">During installation, you can view the domains that have been verified and the ones that have not.</span><span class="sxs-lookup"><span data-stu-id="c04c4-136">During installation, you can view the domains that have been verified and the ones that have not.</span></span>

   ![Unverified domains](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png) 

## <a name="alternate-login-id"></a><span data-ttu-id="c04c4-138">Alternate login ID</span><span class="sxs-lookup"><span data-stu-id="c04c4-138">Alternate login ID</span></span>
<span data-ttu-id="c04c4-139">In some environments, end users may only be aware of their email address and not their UPN.</span><span class="sxs-lookup"><span data-stu-id="c04c4-139">In some environments, end users may only be aware of their email address and not their UPN.</span></span>  <span data-ttu-id="c04c4-140">The use of email address may be due to a corporate policy or an on-premises line-of-business application dependency.</span><span class="sxs-lookup"><span data-stu-id="c04c4-140">The use of email address may be due to a corporate policy or an on-premises line-of-business application dependency.</span></span>

<span data-ttu-id="c04c4-141">Alternate login ID allows you to configure a sign-in experience where users can sign-in with an attribute other than their UPN, such as mail.</span><span class="sxs-lookup"><span data-stu-id="c04c4-141">Alternate login ID allows you to configure a sign-in experience where users can sign-in with an attribute other than their UPN, such as mail.</span></span>

<span data-ttu-id="c04c4-142">To enable Alternate login ID with Azure AD, no additional configurations steps are needed when using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c04c4-142">To enable Alternate login ID with Azure AD, no additional configurations steps are needed when using Azure AD Connect.</span></span> <span data-ttu-id="c04c4-143">Alternate ID can be configured directly from the wizard.</span><span class="sxs-lookup"><span data-stu-id="c04c4-143">Alternate ID can be configured directly from the wizard.</span></span> <span data-ttu-id="c04c4-144">See Azure AD sign-in configuration for your users under the section Sync. Under the **User Principal Name** drop-down, select the attribute for Alternate login ID.</span><span class="sxs-lookup"><span data-stu-id="c04c4-144">See Azure AD sign-in configuration for your users under the section Sync. Under the **User Principal Name** drop-down, select the attribute for Alternate login ID.</span></span>

![Unverified domains](./media/active-directory-aadconnect-userprincipalname/altloginid.png)  

<span data-ttu-id="c04c4-146">For more information, see [Configure Alternate login ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) and [Azure AD sign-in configuration](active-directory-aadconnect-get-started-custom.md#azure-ad-sign-in-configuration)</span><span class="sxs-lookup"><span data-stu-id="c04c4-146">For more information, see [Configure Alternate login ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) and [Azure AD sign-in configuration](active-directory-aadconnect-get-started-custom.md#azure-ad-sign-in-configuration)</span></span>

## <a name="non-verified-upn-suffix"></a><span data-ttu-id="c04c4-147">Non-verified UPN Suffix</span><span class="sxs-lookup"><span data-stu-id="c04c4-147">Non-verified UPN Suffix</span></span>
<span data-ttu-id="c04c4-148">If the on-premises UserPrincipalName attribute/Alternate login ID suffix is not verified with Azure AD Tenant, then the Azure AD UserPrincipalName attribute value is set to MOERA.</span><span class="sxs-lookup"><span data-stu-id="c04c4-148">If the on-premises UserPrincipalName attribute/Alternate login ID suffix is not verified with Azure AD Tenant, then the Azure AD UserPrincipalName attribute value is set to MOERA.</span></span> <span data-ttu-id="c04c4-149">Azure AD calculates the MOERA from the Azure AD MailNickName attribute and Azure AD initial domain as &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span><span class="sxs-lookup"><span data-stu-id="c04c4-149">Azure AD calculates the MOERA from the Azure AD MailNickName attribute and Azure AD initial domain as &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span></span>

## <a name="verified-upn-suffix"></a><span data-ttu-id="c04c4-150">Verified UPN suffix</span><span class="sxs-lookup"><span data-stu-id="c04c4-150">Verified UPN suffix</span></span>
<span data-ttu-id="c04c4-151">If the on-premises UserPrincipalName attribute/Alternate login ID suffix is verified with the Azure AD Tenant, then the Azure AD UserPrincipalName attribute value is going to be the same as the on-premises UserPrincipalName attribute/Alternate login ID value.</span><span class="sxs-lookup"><span data-stu-id="c04c4-151">If the on-premises UserPrincipalName attribute/Alternate login ID suffix is verified with the Azure AD Tenant, then the Azure AD UserPrincipalName attribute value is going to be the same as the on-premises UserPrincipalName attribute/Alternate login ID value.</span></span>

## <a name="azure-ad-mailnickname-attribute-value-calculation"></a><span data-ttu-id="c04c4-152">Azure AD MailNickName attribute value calculation</span><span class="sxs-lookup"><span data-stu-id="c04c4-152">Azure AD MailNickName attribute value calculation</span></span>
<span data-ttu-id="c04c4-153">Because the Azure AD UserPrincipalName attribute value could be set to MOERA, it is important to understand how the Azure AD MailNickName attribute value, which is the MOERA prefix, is calculated.</span><span class="sxs-lookup"><span data-stu-id="c04c4-153">Because the Azure AD UserPrincipalName attribute value could be set to MOERA, it is important to understand how the Azure AD MailNickName attribute value, which is the MOERA prefix, is calculated.</span></span>

<span data-ttu-id="c04c4-154">When a user object is synchronized to an Azure AD Tenant for the first time, Azure AD checks the following items in the given order and sets the MailNickName attribute value to the first existing one:</span><span class="sxs-lookup"><span data-stu-id="c04c4-154">When a user object is synchronized to an Azure AD Tenant for the first time, Azure AD checks the following items in the given order and sets the MailNickName attribute value to the first existing one:</span></span>

- <span data-ttu-id="c04c4-155">On-premises mailNickName attribute</span><span class="sxs-lookup"><span data-stu-id="c04c4-155">On-premises mailNickName attribute</span></span>
- <span data-ttu-id="c04c4-156">Prefix of primary SMTP address</span><span class="sxs-lookup"><span data-stu-id="c04c4-156">Prefix of primary SMTP address</span></span>
- <span data-ttu-id="c04c4-157">Prefix of on-premises mail attribute</span><span class="sxs-lookup"><span data-stu-id="c04c4-157">Prefix of on-premises mail attribute</span></span>
- <span data-ttu-id="c04c4-158">Prefix of on-premises userPrincipalName attribute/Alternate login ID</span><span class="sxs-lookup"><span data-stu-id="c04c4-158">Prefix of on-premises userPrincipalName attribute/Alternate login ID</span></span>
- <span data-ttu-id="c04c4-159">Prefix of secondary smtp address</span><span class="sxs-lookup"><span data-stu-id="c04c4-159">Prefix of secondary smtp address</span></span>

<span data-ttu-id="c04c4-160">When the updates to a user object are synchronized to the Azure AD Tenant, Azure AD updates the MailNickName attribute value only in case there is an update to the on-premises mailNickName attribute value.</span><span class="sxs-lookup"><span data-stu-id="c04c4-160">When the updates to a user object are synchronized to the Azure AD Tenant, Azure AD updates the MailNickName attribute value only in case there is an update to the on-premises mailNickName attribute value.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c04c4-161">Azure AD recalculates the UserPrincipalName attribute value only in case an update to the on-premises UserPrincipalName attribute/Alternate login ID value is synchronized to the Azure AD Tenant.</span><span class="sxs-lookup"><span data-stu-id="c04c4-161">Azure AD recalculates the UserPrincipalName attribute value only in case an update to the on-premises UserPrincipalName attribute/Alternate login ID value is synchronized to the Azure AD Tenant.</span></span> 
>
><span data-ttu-id="c04c4-162">Whenever Azure AD recalculates the UserPrincipalName attribute, it also recalculates the MOERA.</span><span class="sxs-lookup"><span data-stu-id="c04c4-162">Whenever Azure AD recalculates the UserPrincipalName attribute, it also recalculates the MOERA.</span></span> 

## <a name="upn-scenarios"></a><span data-ttu-id="c04c4-163">UPN scenarios</span><span class="sxs-lookup"><span data-stu-id="c04c4-163">UPN scenarios</span></span>
<span data-ttu-id="c04c4-164">The following are example scenarios of how the UPN is calculated based on the given scenario.</span><span class="sxs-lookup"><span data-stu-id="c04c4-164">The following are example scenarios of how the UPN is calculated based on the given scenario.</span></span>

### <a name="scenario-1-non-verified-upn-suffix--initial-synchronization"></a><span data-ttu-id="c04c4-165">Scenario 1: Non-verified UPN suffix – initial synchronization</span><span class="sxs-lookup"><span data-stu-id="c04c4-165">Scenario 1: Non-verified UPN suffix – initial synchronization</span></span>

![Scenario1](media/active-directory-aadconnect-userprincipalname/example1.png)

<span data-ttu-id="c04c4-167">On-Premises user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-167">On-Premises user object:</span></span>
- <span data-ttu-id="c04c4-168">mailNickName      : &lt;not set&gt;</span><span class="sxs-lookup"><span data-stu-id="c04c4-168">mailNickName      : &lt;not set&gt;</span></span>
- <span data-ttu-id="c04c4-169">proxyAddresses        : {SMTP:us1@contoso.com}</span><span class="sxs-lookup"><span data-stu-id="c04c4-169">proxyAddresses        : {SMTP:us1@contoso.com}</span></span>
- <span data-ttu-id="c04c4-170">mail          : us2@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-170">mail          : us2@contoso.com</span></span>
- <span data-ttu-id="c04c4-171">userPrincipalName : us3@contoso.com\`</span><span class="sxs-lookup"><span data-stu-id="c04c4-171">userPrincipalName : us3@contoso.com\`</span></span>

<span data-ttu-id="c04c4-172">Synchronized the user object to Azure AD Tenant for the first time</span><span class="sxs-lookup"><span data-stu-id="c04c4-172">Synchronized the user object to Azure AD Tenant for the first time</span></span>
- <span data-ttu-id="c04c4-173">Set Azure AD MailNickName attribute to primary SMTP address prefix.</span><span class="sxs-lookup"><span data-stu-id="c04c4-173">Set Azure AD MailNickName attribute to primary SMTP address prefix.</span></span>
- <span data-ttu-id="c04c4-174">Set MOERA to  &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span><span class="sxs-lookup"><span data-stu-id="c04c4-174">Set MOERA to  &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span></span>
- <span data-ttu-id="c04c4-175">Set Azure AD UserPrincipalName attribute to MOERA.</span><span class="sxs-lookup"><span data-stu-id="c04c4-175">Set Azure AD UserPrincipalName attribute to MOERA.</span></span>

<span data-ttu-id="c04c4-176">Azure AD Tenant user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-176">Azure AD Tenant user object:</span></span>
- <span data-ttu-id="c04c4-177">MailNickName      : us1</span><span class="sxs-lookup"><span data-stu-id="c04c4-177">MailNickName      : us1</span></span>           
- <span data-ttu-id="c04c4-178">UserPrincipalName : us1@contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-178">UserPrincipalName : us1@contoso.onmicrosoft.com</span></span>


### <a name="scenario-2-non-verified-upn-suffix--set-on-premises-mailnickname-attribute"></a><span data-ttu-id="c04c4-179">Scenario 2: Non-verified UPN suffix – set on-premises mailNickName attribute</span><span class="sxs-lookup"><span data-stu-id="c04c4-179">Scenario 2: Non-verified UPN suffix – set on-premises mailNickName attribute</span></span>

![Scenario2](media/active-directory-aadconnect-userprincipalname/example2.png)

<span data-ttu-id="c04c4-181">On-Premises user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-181">On-Premises user object:</span></span>
- <span data-ttu-id="c04c4-182">mailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-182">mailNickName      : us4</span></span>
- <span data-ttu-id="c04c4-183">proxyAddresses        : {SMTP:us1@contoso.com}</span><span class="sxs-lookup"><span data-stu-id="c04c4-183">proxyAddresses        : {SMTP:us1@contoso.com}</span></span>
- <span data-ttu-id="c04c4-184">mail          : us2@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-184">mail          : us2@contoso.com</span></span>
- <span data-ttu-id="c04c4-185">userPrincipalName : us3@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-185">userPrincipalName : us3@contoso.com</span></span>

<span data-ttu-id="c04c4-186">Synchronize update on on-premises mailNickName attribute to Azure AD Tenant</span><span class="sxs-lookup"><span data-stu-id="c04c4-186">Synchronize update on on-premises mailNickName attribute to Azure AD Tenant</span></span>
- <span data-ttu-id="c04c4-187">Update Azure AD MailNickName attribute with on-premises mailNickName attribute.</span><span class="sxs-lookup"><span data-stu-id="c04c4-187">Update Azure AD MailNickName attribute with on-premises mailNickName attribute.</span></span>
- <span data-ttu-id="c04c4-188">Because there is no update to the on-premises userPrincipalName attribute, there is no change to the Azure AD UserPrincipalName attribute.</span><span class="sxs-lookup"><span data-stu-id="c04c4-188">Because there is no update to the on-premises userPrincipalName attribute, there is no change to the Azure AD UserPrincipalName attribute.</span></span>

<span data-ttu-id="c04c4-189">Azure AD Tenant user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-189">Azure AD Tenant user object:</span></span>
- <span data-ttu-id="c04c4-190">MailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-190">MailNickName      : us4</span></span>
- <span data-ttu-id="c04c4-191">UserPrincipalName : us1@contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-191">UserPrincipalName : us1@contoso.onmicrosoft.com</span></span>

### <a name="scenario-3-non-verified-upn-suffix--update-on-premises-userprincipalname-attribute"></a><span data-ttu-id="c04c4-192">Scenario 3: Non-verified UPN suffix – update on-premises userPrincipalName attribute</span><span class="sxs-lookup"><span data-stu-id="c04c4-192">Scenario 3: Non-verified UPN suffix – update on-premises userPrincipalName attribute</span></span>

![Scenario3](media/active-directory-aadconnect-userprincipalname/example3.png)

<span data-ttu-id="c04c4-194">On-Premises user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-194">On-Premises user object:</span></span>
- <span data-ttu-id="c04c4-195">mailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-195">mailNickName      : us4</span></span>
- <span data-ttu-id="c04c4-196">proxyAddresses        : {SMTP:us1@contoso.com}</span><span class="sxs-lookup"><span data-stu-id="c04c4-196">proxyAddresses        : {SMTP:us1@contoso.com}</span></span>
- <span data-ttu-id="c04c4-197">mail          : us2@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-197">mail          : us2@contoso.com</span></span>
- <span data-ttu-id="c04c4-198">userPrincipalName : us5@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-198">userPrincipalName : us5@contoso.com</span></span>

<span data-ttu-id="c04c4-199">Synchronize update on on-premises userPrincipalName attribute to Azure AD Tenant</span><span class="sxs-lookup"><span data-stu-id="c04c4-199">Synchronize update on on-premises userPrincipalName attribute to Azure AD Tenant</span></span>
- <span data-ttu-id="c04c4-200">Update on on-premises userPrincipalName attribute triggers recalculation of MOERA and Azure AD UserPrincipalName attribute.</span><span class="sxs-lookup"><span data-stu-id="c04c4-200">Update on on-premises userPrincipalName attribute triggers recalculation of MOERA and Azure AD UserPrincipalName attribute.</span></span>
- <span data-ttu-id="c04c4-201">Set MOERA to &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span><span class="sxs-lookup"><span data-stu-id="c04c4-201">Set MOERA to &lt;MailNickName&gt;&#64;&lt;initial domain&gt;.</span></span>
- <span data-ttu-id="c04c4-202">Set Azure AD UserPrincipalName attribute to MOERA.</span><span class="sxs-lookup"><span data-stu-id="c04c4-202">Set Azure AD UserPrincipalName attribute to MOERA.</span></span>

<span data-ttu-id="c04c4-203">Azure AD Tenant user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-203">Azure AD Tenant user object:</span></span>
- <span data-ttu-id="c04c4-204">MailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-204">MailNickName      : us4</span></span>
- <span data-ttu-id="c04c4-205">UserPrincipalName : us4@contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-205">UserPrincipalName : us4@contoso.onmicrosoft.com</span></span>

### <a name="scenario-4-non-verified-upn-suffix--update-primary-smtp-address-and-on-premises-mail-attribute"></a><span data-ttu-id="c04c4-206">Scenario 4: Non-verified UPN suffix – update primary SMTP address and on-premises mail attribute</span><span class="sxs-lookup"><span data-stu-id="c04c4-206">Scenario 4: Non-verified UPN suffix – update primary SMTP address and on-premises mail attribute</span></span>

![Scenario4](media/active-directory-aadconnect-userprincipalname/example4.png)

<span data-ttu-id="c04c4-208">On-Premises user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-208">On-Premises user object:</span></span>
- <span data-ttu-id="c04c4-209">mailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-209">mailNickName      : us4</span></span>
- <span data-ttu-id="c04c4-210">proxyAddresses        : {SMTP:us6@contoso.com}</span><span class="sxs-lookup"><span data-stu-id="c04c4-210">proxyAddresses        : {SMTP:us6@contoso.com}</span></span>
- <span data-ttu-id="c04c4-211">mail          : us7@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-211">mail          : us7@contoso.com</span></span>
- <span data-ttu-id="c04c4-212">userPrincipalName : us5@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-212">userPrincipalName : us5@contoso.com</span></span>

<span data-ttu-id="c04c4-213">Synchronize update on on-premises mail attribute and primary SMTP address to Azure AD Tenant</span><span class="sxs-lookup"><span data-stu-id="c04c4-213">Synchronize update on on-premises mail attribute and primary SMTP address to Azure AD Tenant</span></span>
- <span data-ttu-id="c04c4-214">After the initial synchronization of the user object, updates to the on-premises mail attribute and the primary SMTP address will not affect the Azure AD MailNickName or the UserPrincipalName attribute.</span><span class="sxs-lookup"><span data-stu-id="c04c4-214">After the initial synchronization of the user object, updates to the on-premises mail attribute and the primary SMTP address will not affect the Azure AD MailNickName or the UserPrincipalName attribute.</span></span>

<span data-ttu-id="c04c4-215">Azure AD Tenant user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-215">Azure AD Tenant user object:</span></span>
- <span data-ttu-id="c04c4-216">MailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-216">MailNickName      : us4</span></span>
- <span data-ttu-id="c04c4-217">UserPrincipalName : us4@contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-217">UserPrincipalName : us4@contoso.onmicrosoft.com</span></span>

### <a name="scenario-5-verified-upn-suffix--update-on-premises-userprincipalname-attribute-suffix"></a><span data-ttu-id="c04c4-218">Scenario 5: Verified UPN suffix – update on-premises userPrincipalName attribute suffix</span><span class="sxs-lookup"><span data-stu-id="c04c4-218">Scenario 5: Verified UPN suffix – update on-premises userPrincipalName attribute suffix</span></span>

![Scenario5](media/active-directory-aadconnect-userprincipalname/example5.png)

<span data-ttu-id="c04c4-220">On-Premises user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-220">On-Premises user object:</span></span>
- <span data-ttu-id="c04c4-221">mailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-221">mailNickName      : us4</span></span>
- <span data-ttu-id="c04c4-222">proxyAddresses        : {SMTP:us6@contoso.com}</span><span class="sxs-lookup"><span data-stu-id="c04c4-222">proxyAddresses        : {SMTP:us6@contoso.com}</span></span>
- <span data-ttu-id="c04c4-223">mail          : us7@contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-223">mail          : us7@contoso.com</span></span>
- <span data-ttu-id="c04c4-224">serPrincipalName  : us5@verified.contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-224">serPrincipalName  : us5@verified.contoso.com</span></span>

<span data-ttu-id="c04c4-225">Synchronize update on on-premises userPrincipalName attribute to the Azure AD Tenant</span><span class="sxs-lookup"><span data-stu-id="c04c4-225">Synchronize update on on-premises userPrincipalName attribute to the Azure AD Tenant</span></span>
- <span data-ttu-id="c04c4-226">Update on on-premises userPrincipalName attribute triggers recalculation of Azure AD UserPrincipalName attribute.</span><span class="sxs-lookup"><span data-stu-id="c04c4-226">Update on on-premises userPrincipalName attribute triggers recalculation of Azure AD UserPrincipalName attribute.</span></span>
- <span data-ttu-id="c04c4-227">Set Azure AD UserPrincipalName attribute to on-premises userPrincipalName attribute as the UPN suffix is verified with the Azure AD Tenant.</span><span class="sxs-lookup"><span data-stu-id="c04c4-227">Set Azure AD UserPrincipalName attribute to on-premises userPrincipalName attribute as the UPN suffix is verified with the Azure AD Tenant.</span></span>

<span data-ttu-id="c04c4-228">Azure AD Tenant user object:</span><span class="sxs-lookup"><span data-stu-id="c04c4-228">Azure AD Tenant user object:</span></span>
- <span data-ttu-id="c04c4-229">MailNickName      : us4</span><span class="sxs-lookup"><span data-stu-id="c04c4-229">MailNickName      : us4</span></span>     
- <span data-ttu-id="c04c4-230">UserPrincipalName : us5@verified.contoso.com</span><span class="sxs-lookup"><span data-stu-id="c04c4-230">UserPrincipalName : us5@verified.contoso.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="c04c4-231">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c04c4-231">Next Steps</span></span>
- [<span data-ttu-id="c04c4-232">Integrate your on-premises directories with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c04c4-232">Integrate your on-premises directories with Azure Active Directory</span></span>](active-directory-aadconnect.md)
- [<span data-ttu-id="c04c4-233">Custom installation of Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c04c4-233">Custom installation of Azure AD Connect</span></span>](active-directory-aadconnect-get-started-custom.md)
