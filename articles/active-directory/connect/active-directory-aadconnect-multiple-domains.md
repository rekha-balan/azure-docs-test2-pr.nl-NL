---
title: Azure AD Connect Multiple Domains
description: This document describes setting up and configuring multiple top level domains with O365 and Azure AD.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: billmath
ms.openlocfilehash: ad5227e5a5b7bcbe48b4d5ec9fff67bb7f51b2fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540946"
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="da960-103">Multiple Domain Support for Federating with Azure AD</span><span class="sxs-lookup"><span data-stu-id="da960-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="da960-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span><span class="sxs-lookup"><span data-stu-id="da960-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="da960-105">Multiple top-level domain support</span><span class="sxs-lookup"><span data-stu-id="da960-105">Multiple top-level domain support</span></span>
<span data-ttu-id="da960-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span><span class="sxs-lookup"><span data-stu-id="da960-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="da960-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span><span class="sxs-lookup"><span data-stu-id="da960-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="da960-108">One important one is IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="da960-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="da960-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span><span class="sxs-lookup"><span data-stu-id="da960-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="da960-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span><span class="sxs-lookup"><span data-stu-id="da960-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="da960-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="da960-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="da960-112">The federation service identifier is a URI that uniquely identifies a federation service.</span><span class="sxs-lookup"><span data-stu-id="da960-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="da960-113">The federation service is an instance of AD FS that functions as the security token service.</span><span class="sxs-lookup"><span data-stu-id="da960-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="da960-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="da960-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="da960-116">A problem arises when we want to add more than one top-level domain.</span><span class="sxs-lookup"><span data-stu-id="da960-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="da960-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="da960-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="da960-118">For this document I am using bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="da960-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="da960-119">Now I have added a second, top-level domain, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="da960-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domains](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="da960-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span><span class="sxs-lookup"><span data-stu-id="da960-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="da960-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span><span class="sxs-lookup"><span data-stu-id="da960-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![Federation error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="da960-124">SupportMultipleDomain Parameter</span><span class="sxs-lookup"><span data-stu-id="da960-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="da960-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span><span class="sxs-lookup"><span data-stu-id="da960-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="da960-126">This parameter is used with the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="da960-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="da960-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span><span class="sxs-lookup"><span data-stu-id="da960-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="da960-128">This will be unique across directories in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da960-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="da960-129">Using the parameter allows the PowerShell command to complete successfully.</span><span class="sxs-lookup"><span data-stu-id="da960-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![Federation error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="da960-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span><span class="sxs-lookup"><span data-stu-id="da960-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![Federation error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="da960-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="da960-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="da960-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da960-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="da960-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="da960-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="da960-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da960-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="da960-137">If a match cannot be found the authentication will fail.</span><span class="sxs-lookup"><span data-stu-id="da960-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="da960-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="da960-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="da960-139">This will match the Azure AD configuration, and authentication will succeed.</span><span class="sxs-lookup"><span data-stu-id="da960-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="da960-140">The following is the customized claim rule that implements this logic:</span><span class="sxs-lookup"><span data-stu-id="da960-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="da960-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span><span class="sxs-lookup"><span data-stu-id="da960-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="da960-142">How to update the trust between AD FS and Azure AD</span><span class="sxs-lookup"><span data-stu-id="da960-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="da960-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span><span class="sxs-lookup"><span data-stu-id="da960-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="da960-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span><span class="sxs-lookup"><span data-stu-id="da960-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="da960-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="da960-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="da960-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span><span class="sxs-lookup"><span data-stu-id="da960-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![Federation error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="da960-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span><span class="sxs-lookup"><span data-stu-id="da960-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![Federation error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="da960-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span><span class="sxs-lookup"><span data-stu-id="da960-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![Federation error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="da960-152">Use the steps below to add an additional top-level domain.</span><span class="sxs-lookup"><span data-stu-id="da960-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="da960-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span><span class="sxs-lookup"><span data-stu-id="da960-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="da960-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="da960-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="da960-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span><span class="sxs-lookup"><span data-stu-id="da960-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="da960-156">On your AD FS federation server open **AD FS Management.**</span><span class="sxs-lookup"><span data-stu-id="da960-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="da960-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span><span class="sxs-lookup"><span data-stu-id="da960-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="da960-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span><span class="sxs-lookup"><span data-stu-id="da960-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="da960-159">![Remove Microsoft Online](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="da960-159">![Remove Microsoft Online](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="da960-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="da960-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="da960-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span><span class="sxs-lookup"><span data-stu-id="da960-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="da960-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="da960-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="da960-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="da960-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="da960-164">This is for the original domain.</span><span class="sxs-lookup"><span data-stu-id="da960-164">This is for the original domain.</span></span>  <span data-ttu-id="da960-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="da960-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="da960-166">Use the following steps to add the new top-level domain using PowerShell</span><span class="sxs-lookup"><span data-stu-id="da960-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="da960-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="da960-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="da960-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span><span class="sxs-lookup"><span data-stu-id="da960-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="da960-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="da960-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="da960-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="da960-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="da960-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="da960-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="da960-172">Launch Azure AD Connect from the desktop or start menu</span><span class="sxs-lookup"><span data-stu-id="da960-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="da960-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="da960-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="da960-174">Enter your Azure AD and Active Directory credentials</span><span class="sxs-lookup"><span data-stu-id="da960-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="da960-175">Select the second domain you wish to configure for federation.</span><span class="sxs-lookup"><span data-stu-id="da960-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="da960-176">![Add an additional Azure AD domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="da960-176">![Add an additional Azure AD domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="da960-177">Click Install</span><span class="sxs-lookup"><span data-stu-id="da960-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="da960-178">Verify the new top-level domain</span><span class="sxs-lookup"><span data-stu-id="da960-178">Verify the new top-level domain</span></span>
<span data-ttu-id="da960-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="da960-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="da960-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="da960-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="da960-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="da960-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="da960-184">Support for Sub-domains</span><span class="sxs-lookup"><span data-stu-id="da960-184">Support for Sub-domains</span></span>
<span data-ttu-id="da960-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span><span class="sxs-lookup"><span data-stu-id="da960-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="da960-186">This means that the IssuerUri needs to match the parents.</span><span class="sxs-lookup"><span data-stu-id="da960-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="da960-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="da960-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="da960-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="da960-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="da960-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="da960-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="da960-190">which will not match the domain's required value and authentication will fail.</span><span class="sxs-lookup"><span data-stu-id="da960-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="da960-191">How To enable support for sub-domains</span><span class="sxs-lookup"><span data-stu-id="da960-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="da960-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span><span class="sxs-lookup"><span data-stu-id="da960-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="da960-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span><span class="sxs-lookup"><span data-stu-id="da960-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="da960-194">The following claim will do this:</span><span class="sxs-lookup"><span data-stu-id="da960-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="da960-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span><span class="sxs-lookup"><span data-stu-id="da960-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="da960-196">Here i have bmcontoso.com so two parent domains are necessary.</span><span class="sxs-lookup"><span data-stu-id="da960-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="da960-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span><span class="sxs-lookup"><span data-stu-id="da960-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="da960-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span><span class="sxs-lookup"><span data-stu-id="da960-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="da960-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="da960-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="da960-200">Use the following steps to add a custom claim to support sub-domains.</span><span class="sxs-lookup"><span data-stu-id="da960-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="da960-201">Open AD FS Management</span><span class="sxs-lookup"><span data-stu-id="da960-201">Open AD FS Management</span></span>
2. <span data-ttu-id="da960-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span><span class="sxs-lookup"><span data-stu-id="da960-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="da960-203">Select the third claim rule, and replace ![Edit claim](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="da960-203">Select the third claim rule, and replace ![Edit claim](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="da960-204">Replace the current claim:</span><span class="sxs-lookup"><span data-stu-id="da960-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Replace claim](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="da960-206">Click Ok.</span><span class="sxs-lookup"><span data-stu-id="da960-206">Click Ok.</span></span>  <span data-ttu-id="da960-207">Click Apply.</span><span class="sxs-lookup"><span data-stu-id="da960-207">Click Apply.</span></span>  <span data-ttu-id="da960-208">Click Ok.</span><span class="sxs-lookup"><span data-stu-id="da960-208">Click Ok.</span></span>  <span data-ttu-id="da960-209">Close AD FS Management.</span><span class="sxs-lookup"><span data-stu-id="da960-209">Close AD FS Management.</span></span>
















