---
title: Conditional access to on-prem apps - Azure AD | Microsoft Docs
description: Covers how to set up conditional access for applications you publish to be accessed remotely using Azure AD Application Proxy.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: kgremban
ms.openlocfilehash: 9486bce7d3b510cb3a6bad8f6b504c586dd104c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563130"
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a><span data-ttu-id="7cd78-103">Working with conditional access in Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="7cd78-103">Working with conditional access in Azure AD Application Proxy</span></span>
<span data-ttu-id="7cd78-104">You can configure access rules to grant conditional access to applications published using Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="7cd78-104">You can configure access rules to grant conditional access to applications published using Application Proxy.</span></span> <span data-ttu-id="7cd78-105">This enables you to:</span><span class="sxs-lookup"><span data-stu-id="7cd78-105">This enables you to:</span></span>

* <span data-ttu-id="7cd78-106">Require multi-factor authentication per application</span><span class="sxs-lookup"><span data-stu-id="7cd78-106">Require multi-factor authentication per application</span></span>
* <span data-ttu-id="7cd78-107">Require multi-factor authentication only when users are not at work</span><span class="sxs-lookup"><span data-stu-id="7cd78-107">Require multi-factor authentication only when users are not at work</span></span>
* <span data-ttu-id="7cd78-108">Block users from accessing the application when they are not at work</span><span class="sxs-lookup"><span data-stu-id="7cd78-108">Block users from accessing the application when they are not at work</span></span>

<span data-ttu-id="7cd78-109">These rules can be applied to all users and groups or only to specific users and groups.</span><span class="sxs-lookup"><span data-stu-id="7cd78-109">These rules can be applied to all users and groups or only to specific users and groups.</span></span> <span data-ttu-id="7cd78-110">By default the rule will apply to all users who have access to the application.</span><span class="sxs-lookup"><span data-stu-id="7cd78-110">By default the rule will apply to all users who have access to the application.</span></span> <span data-ttu-id="7cd78-111">However the rule can also be restricted to users that are members of specified security groups.</span><span class="sxs-lookup"><span data-stu-id="7cd78-111">However the rule can also be restricted to users that are members of specified security groups.</span></span>  

<span data-ttu-id="7cd78-112">Access rules are evaluated when a user accesses a federated application that uses OAuth 2.0, OpenID Connect, SAML or WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="7cd78-112">Access rules are evaluated when a user accesses a federated application that uses OAuth 2.0, OpenID Connect, SAML or WS-Federation.</span></span> <span data-ttu-id="7cd78-113">In addition, access rules are evaluated with OAuth 2.0 and OpenID Connect when a refresh token is used to acquire an access token.</span><span class="sxs-lookup"><span data-stu-id="7cd78-113">In addition, access rules are evaluated with OAuth 2.0 and OpenID Connect when a refresh token is used to acquire an access token.</span></span>

## <a name="conditional-access-prerequisites"></a><span data-ttu-id="7cd78-114">Conditional access prerequisites</span><span class="sxs-lookup"><span data-stu-id="7cd78-114">Conditional access prerequisites</span></span>
* <span data-ttu-id="7cd78-115">Subscription to Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="7cd78-115">Subscription to Azure Active Directory Premium</span></span>
* <span data-ttu-id="7cd78-116">A federated or managed Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="7cd78-116">A federated or managed Azure Active Directory tenant</span></span>
* <span data-ttu-id="7cd78-117">Federated tenants require that multi-factor authentication (MFA) be enabled</span><span class="sxs-lookup"><span data-stu-id="7cd78-117">Federated tenants require that multi-factor authentication (MFA) be enabled</span></span>  
    ![Configure access rules - require multi-factor authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a><span data-ttu-id="7cd78-119">Configure per-application multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="7cd78-119">Configure per-application multi-factor authentication</span></span>
1. <span data-ttu-id="7cd78-120">Sign in as an administrator in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="7cd78-120">Sign in as an administrator in the Azure classic portal.</span></span>
2. <span data-ttu-id="7cd78-121">Go to Active Directory and select the directory in which you want to enable Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="7cd78-121">Go to Active Directory and select the directory in which you want to enable Application Proxy.</span></span>
3. <span data-ttu-id="7cd78-122">Click **Applications** and scroll down to the **Access Rules** section.</span><span class="sxs-lookup"><span data-stu-id="7cd78-122">Click **Applications** and scroll down to the **Access Rules** section.</span></span> <span data-ttu-id="7cd78-123">The access rules section only appears for applications published using Application Proxy that use federated authentication.</span><span class="sxs-lookup"><span data-stu-id="7cd78-123">The access rules section only appears for applications published using Application Proxy that use federated authentication.</span></span>
4. <span data-ttu-id="7cd78-124">Enable the rule by selecting **Enable Access Rules** to **On**.</span><span class="sxs-lookup"><span data-stu-id="7cd78-124">Enable the rule by selecting **Enable Access Rules** to **On**.</span></span>
5. <span data-ttu-id="7cd78-125">Specify the users and groups to whom the rules will apply.</span><span class="sxs-lookup"><span data-stu-id="7cd78-125">Specify the users and groups to whom the rules will apply.</span></span> <span data-ttu-id="7cd78-126">Use the **Add Group** button  to select one or more groups to which the access rule will apply.</span><span class="sxs-lookup"><span data-stu-id="7cd78-126">Use the **Add Group** button  to select one or more groups to which the access rule will apply.</span></span> <span data-ttu-id="7cd78-127">This dialog can also be used to remove selected groups.</span><span class="sxs-lookup"><span data-stu-id="7cd78-127">This dialog can also be used to remove selected groups.</span></span>  <span data-ttu-id="7cd78-128">When the rules are selected to apply to groups, the access rules will only be enforced for users that belong to one of the specified security groups.</span><span class="sxs-lookup"><span data-stu-id="7cd78-128">When the rules are selected to apply to groups, the access rules will only be enforced for users that belong to one of the specified security groups.</span></span>  

   * <span data-ttu-id="7cd78-129">To explicitly exclude security groups from the rule, check **Except**  and specify one or more groups.</span><span class="sxs-lookup"><span data-stu-id="7cd78-129">To explicitly exclude security groups from the rule, check **Except**  and specify one or more groups.</span></span> <span data-ttu-id="7cd78-130">Users who are members of a group in the Except list will not be required to perform multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="7cd78-130">Users who are members of a group in the Except list will not be required to perform multi-factor authentication.</span></span>  
   * <span data-ttu-id="7cd78-131">If a user was configured using the per-user multi-factor authentication feature, this setting will take precedence over the application multi-factor authentication rules.</span><span class="sxs-lookup"><span data-stu-id="7cd78-131">If a user was configured using the per-user multi-factor authentication feature, this setting will take precedence over the application multi-factor authentication rules.</span></span> <span data-ttu-id="7cd78-132">This means that a user who has been configured for per-user multi-factor authentication will be required to perform multi-factor authentication even if they have been exempted from the application's multi-factor authentication rules.</span><span class="sxs-lookup"><span data-stu-id="7cd78-132">This means that a user who has been configured for per-user multi-factor authentication will be required to perform multi-factor authentication even if they have been exempted from the application's multi-factor authentication rules.</span></span> <span data-ttu-id="7cd78-133">Learn more about [multi-factor authentication and per-user settings](../multi-factor-authentication/multi-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7cd78-133">Learn more about [multi-factor authentication and per-user settings](../multi-factor-authentication/multi-factor-authentication.md).</span></span>
6. <span data-ttu-id="7cd78-134">Select the access rule you want to set:</span><span class="sxs-lookup"><span data-stu-id="7cd78-134">Select the access rule you want to set:</span></span>

   * <span data-ttu-id="7cd78-135">**Require Multi-factor authentication**: Users to whom access rules apply will be required to complete multi-factor authentication before accessing the application to which the rule applies.</span><span class="sxs-lookup"><span data-stu-id="7cd78-135">**Require Multi-factor authentication**: Users to whom access rules apply will be required to complete multi-factor authentication before accessing the application to which the rule applies.</span></span>
   * <span data-ttu-id="7cd78-136">**Require Multi-factor authentication when not at work**: Users trying to access the application from a trusted IP address will not be required to perform multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="7cd78-136">**Require Multi-factor authentication when not at work**: Users trying to access the application from a trusted IP address will not be required to perform multi-factor authentication.</span></span> <span data-ttu-id="7cd78-137">The trusted IP address ranges can be configured on the multi-factor authentication settings page.</span><span class="sxs-lookup"><span data-stu-id="7cd78-137">The trusted IP address ranges can be configured on the multi-factor authentication settings page.</span></span>
   * <span data-ttu-id="7cd78-138">**Block access when not at work**: Users trying to access the application from outside your corporate network will not be able to access the application.</span><span class="sxs-lookup"><span data-stu-id="7cd78-138">**Block access when not at work**: Users trying to access the application from outside your corporate network will not be able to access the application.</span></span>

## <a name="configuring-mfa-for-federation-services"></a><span data-ttu-id="7cd78-139">Configuring MFA for federation services</span><span class="sxs-lookup"><span data-stu-id="7cd78-139">Configuring MFA for federation services</span></span>
<span data-ttu-id="7cd78-140">For federated tenants, multi-factor authentication (MFA) may be performed by Azure Active Directory or by the on-premises AD FS server.</span><span class="sxs-lookup"><span data-stu-id="7cd78-140">For federated tenants, multi-factor authentication (MFA) may be performed by Azure Active Directory or by the on-premises AD FS server.</span></span> <span data-ttu-id="7cd78-141">By default, MFA will occur on any page hosted by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7cd78-141">By default, MFA will occur on any page hosted by Azure Active Directory.</span></span> <span data-ttu-id="7cd78-142">In order to configure MFA on-premises, run Windows PowerShell and use the –SupportsMFA property to set the Azure AD module.</span><span class="sxs-lookup"><span data-stu-id="7cd78-142">In order to configure MFA on-premises, run Windows PowerShell and use the –SupportsMFA property to set the Azure AD module.</span></span>

<span data-ttu-id="7cd78-143">The following example shows how to enable on-premises MFA by using the [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) on the contoso.com tenant: `Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `</span><span class="sxs-lookup"><span data-stu-id="7cd78-143">The following example shows how to enable on-premises MFA by using the [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) on the contoso.com tenant: `Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `</span></span>

<span data-ttu-id="7cd78-144">In addition to setting this flag, the federated tenant AD FS instance must be configured to perform multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="7cd78-144">In addition to setting this flag, the federated tenant AD FS instance must be configured to perform multi-factor authentication.</span></span> <span data-ttu-id="7cd78-145">Follow the instructions for [deploying Microsoft Azure multi-factor authentication on-premises](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span><span class="sxs-lookup"><span data-stu-id="7cd78-145">Follow the instructions for [deploying Microsoft Azure multi-factor authentication on-premises](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7cd78-146">See also</span><span class="sxs-lookup"><span data-stu-id="7cd78-146">See also</span></span>
* [<span data-ttu-id="7cd78-147">Working with claims aware applications</span><span class="sxs-lookup"><span data-stu-id="7cd78-147">Working with claims aware applications</span></span>](active-directory-application-proxy-claims-aware-apps.md)
* [<span data-ttu-id="7cd78-148">Publish applications with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="7cd78-148">Publish applications with Application Proxy</span></span>](active-directory-application-proxy-publish.md)
* [<span data-ttu-id="7cd78-149">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="7cd78-149">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="7cd78-150">Publish applications using your own domain name</span><span class="sxs-lookup"><span data-stu-id="7cd78-150">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)

<span data-ttu-id="7cd78-151">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="7cd78-151">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
