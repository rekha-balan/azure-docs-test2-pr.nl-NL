---
title: Get started integrating Azure AD with apps | Microsoft Docs
description: This article is a getting started guide for integrating Azure Active Directory (AD) with on-premises applications, and cloud applications.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: app-mgmt
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/16/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: d52ec316f9f5540d4d0d0fe0bc4e4bf778e1daf7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869598"
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a><span data-ttu-id="ff8a0-103">Integrating Azure Active Directory with applications getting started guide</span><span class="sxs-lookup"><span data-stu-id="ff8a0-103">Integrating Azure Active Directory with applications getting started guide</span></span>

<span data-ttu-id="ff8a0-104">This topic summarizes the process for integrating applications with Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-104">This topic summarizes the process for integrating applications with Azure Active Directory (AD).</span></span> <span data-ttu-id="ff8a0-105">Each of the sections below contain a brief summary of a more detailed topic so you can identify which parts of this getting started guide are relevant to you.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-105">Each of the sections below contain a brief summary of a more detailed topic so you can identify which parts of this getting started guide are relevant to you.</span></span>

<span data-ttu-id="ff8a0-106">To download in-depth deployment plans, see [Next steps](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-106">To download in-depth deployment plans, see [Next steps](#next-steps).</span></span>

## <a name="take-inventory"></a><span data-ttu-id="ff8a0-107">Take inventory</span><span class="sxs-lookup"><span data-stu-id="ff8a0-107">Take inventory</span></span>
<span data-ttu-id="ff8a0-108">Before integrating applications with Azure AD, it is important to know where you are and where you want to go.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-108">Before integrating applications with Azure AD, it is important to know where you are and where you want to go.</span></span>  <span data-ttu-id="ff8a0-109">The following questions are intended to help you think about your Azure AD application integration project.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-109">The following questions are intended to help you think about your Azure AD application integration project.</span></span>

### <a name="application-inventory"></a><span data-ttu-id="ff8a0-110">Application inventory</span><span class="sxs-lookup"><span data-stu-id="ff8a0-110">Application inventory</span></span>
* <span data-ttu-id="ff8a0-111">Where are all of your applications?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-111">Where are all of your applications?</span></span> <span data-ttu-id="ff8a0-112">Who owns them?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-112">Who owns them?</span></span>
* <span data-ttu-id="ff8a0-113">What kind of authentication do your applications require?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-113">What kind of authentication do your applications require?</span></span>
* <span data-ttu-id="ff8a0-114">Who needs access to which applications?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-114">Who needs access to which applications?</span></span>
* <span data-ttu-id="ff8a0-115">Do you want to deploy a new application?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-115">Do you want to deploy a new application?</span></span>
  * <span data-ttu-id="ff8a0-116">Will you build it in-house and deploy it on an Azure compute instance?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-116">Will you build it in-house and deploy it on an Azure compute instance?</span></span>
  * <span data-ttu-id="ff8a0-117">Will you use one that is available in the Azure Application Gallery?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-117">Will you use one that is available in the Azure Application Gallery?</span></span>

### <a name="user-and-group-inventory"></a><span data-ttu-id="ff8a0-118">User and group inventory</span><span class="sxs-lookup"><span data-stu-id="ff8a0-118">User and group inventory</span></span>
* <span data-ttu-id="ff8a0-119">Where do your user accounts reside?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-119">Where do your user accounts reside?</span></span>
  * <span data-ttu-id="ff8a0-120">On-premises Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff8a0-120">On-premises Active Directory</span></span>
  * <span data-ttu-id="ff8a0-121">Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff8a0-121">Azure AD</span></span>
  * <span data-ttu-id="ff8a0-122">Within a separate application database that you own</span><span class="sxs-lookup"><span data-stu-id="ff8a0-122">Within a separate application database that you own</span></span>
  * <span data-ttu-id="ff8a0-123">In unsanctioned applications</span><span class="sxs-lookup"><span data-stu-id="ff8a0-123">In unsanctioned applications</span></span>
  * <span data-ttu-id="ff8a0-124">All of the above</span><span class="sxs-lookup"><span data-stu-id="ff8a0-124">All of the above</span></span>
* <span data-ttu-id="ff8a0-125">What permissions and role assignments do individual users currently have?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-125">What permissions and role assignments do individual users currently have?</span></span> <span data-ttu-id="ff8a0-126">Do you need to review their access or are you sure that your user access and role assignments are appropriate now?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-126">Do you need to review their access or are you sure that your user access and role assignments are appropriate now?</span></span>
* <span data-ttu-id="ff8a0-127">Are groups already established in your on-premises Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-127">Are groups already established in your on-premises Active Directory?</span></span>
  * <span data-ttu-id="ff8a0-128">How are your groups organized?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-128">How are your groups organized?</span></span>
  * <span data-ttu-id="ff8a0-129">Who are the group members?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-129">Who are the group members?</span></span>
  * <span data-ttu-id="ff8a0-130">What permissions/role assignments do the groups currently have?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-130">What permissions/role assignments do the groups currently have?</span></span>
* <span data-ttu-id="ff8a0-131">Will you need to clean up user/group databases before integrating?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-131">Will you need to clean up user/group databases before integrating?</span></span>  <span data-ttu-id="ff8a0-132">(This is a pretty important question.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-132">(This is a pretty important question.</span></span> <span data-ttu-id="ff8a0-133">Garbage in, garbage out.)</span><span class="sxs-lookup"><span data-stu-id="ff8a0-133">Garbage in, garbage out.)</span></span>

### <a name="access-management-inventory"></a><span data-ttu-id="ff8a0-134">Access management inventory</span><span class="sxs-lookup"><span data-stu-id="ff8a0-134">Access management inventory</span></span>
* <span data-ttu-id="ff8a0-135">How do you currently manage user access to applications?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-135">How do you currently manage user access to applications?</span></span> <span data-ttu-id="ff8a0-136">Does that need to change?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-136">Does that need to change?</span></span>  <span data-ttu-id="ff8a0-137">Have you considered other ways to manage access, such as with [RBAC](../../role-based-access-control/role-assignments-portal.md) for example?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-137">Have you considered other ways to manage access, such as with [RBAC](../../role-based-access-control/role-assignments-portal.md) for example?</span></span>
* <span data-ttu-id="ff8a0-138">Who needs access to what?</span><span class="sxs-lookup"><span data-stu-id="ff8a0-138">Who needs access to what?</span></span>

<span data-ttu-id="ff8a0-139">Maybe you don't have the answers to all of these questions up front but that's okay.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-139">Maybe you don't have the answers to all of these questions up front but that's okay.</span></span>  <span data-ttu-id="ff8a0-140">This guide can help you answer some of those questions and make some informed decisions.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-140">This guide can help you answer some of those questions and make some informed decisions.</span></span>

### <a name="find-unsanctioned-cloud-applications-with-cloud-discovery"></a><span data-ttu-id="ff8a0-141">Find unsanctioned cloud applications with Cloud Discovery</span><span class="sxs-lookup"><span data-stu-id="ff8a0-141">Find unsanctioned cloud applications with Cloud Discovery</span></span>

<span data-ttu-id="ff8a0-142">As mentioned above, there may be applications that haven't been managed by your organization until now.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-142">As mentioned above, there may be applications that haven't been managed by your organization until now.</span></span>  <span data-ttu-id="ff8a0-143">As part of the inventory process, it is possible to find unsanctioned cloud applications.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-143">As part of the inventory process, it is possible to find unsanctioned cloud applications.</span></span> <span data-ttu-id="ff8a0-144">See [Set up Cloud Discovery](/cloud-app-security/set-up-cloud-discovery).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-144">See [Set up Cloud Discovery](/cloud-app-security/set-up-cloud-discovery).</span></span>

## <a name="integrating-applications-with-azure-ad"></a><span data-ttu-id="ff8a0-145">Integrating applications with Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff8a0-145">Integrating applications with Azure AD</span></span>
<span data-ttu-id="ff8a0-146">The following articles discuss the different ways applications integrate with Azure AD, and provide some guidance.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-146">The following articles discuss the different ways applications integrate with Azure AD, and provide some guidance.</span></span>

* [<span data-ttu-id="ff8a0-147">Determining which Active Directory to use</span><span class="sxs-lookup"><span data-stu-id="ff8a0-147">Determining which Active Directory to use</span></span>](../fundamentals/active-directory-administer.md)
* [<span data-ttu-id="ff8a0-148">Using applications in the Azure application gallery</span><span class="sxs-lookup"><span data-stu-id="ff8a0-148">Using applications in the Azure application gallery</span></span>](what-is-single-sign-on.md)
* [<span data-ttu-id="ff8a0-149">Integrating SaaS applications tutorials list</span><span class="sxs-lookup"><span data-stu-id="ff8a0-149">Integrating SaaS applications tutorials list</span></span>](../active-directory-saas-tutorial-list.md)

### <a name="authentication-types"></a><span data-ttu-id="ff8a0-150">Authentication Types</span><span class="sxs-lookup"><span data-stu-id="ff8a0-150">Authentication Types</span></span>
<span data-ttu-id="ff8a0-151">Each of your applications may have different authentication requirements.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-151">Each of your applications may have different authentication requirements.</span></span> <span data-ttu-id="ff8a0-152">With Azure AD, signing certificates can be used with applications that use SAML 2.0, WS-Federation, or OpenID Connect Protocols as well as Password Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-152">With Azure AD, signing certificates can be used with applications that use SAML 2.0, WS-Federation, or OpenID Connect Protocols as well as Password Single Sign On.</span></span> <span data-ttu-id="ff8a0-153">For more information about application authentication types for use with Azure AD see [Managing Certificates for Federated Single Sign-On in Azure Active Directory](manage-certificates-for-federated-single-sign-on.md) and [Password based single sign on](what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-153">For more information about application authentication types for use with Azure AD see [Managing Certificates for Federated Single Sign-On in Azure Active Directory](manage-certificates-for-federated-single-sign-on.md) and [Password based single sign on](what-is-single-sign-on.md).</span></span>

### <a name="enabling-sso-with-azure-ad-app-proxy"></a><span data-ttu-id="ff8a0-154">Enabling SSO with Azure AD App Proxy</span><span class="sxs-lookup"><span data-stu-id="ff8a0-154">Enabling SSO with Azure AD App Proxy</span></span>
<span data-ttu-id="ff8a0-155">With Microsoft Azure AD Application Proxy, you can provide access to applications located inside your private network securely, from anywhere and on any device.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-155">With Microsoft Azure AD Application Proxy, you can provide access to applications located inside your private network securely, from anywhere and on any device.</span></span> <span data-ttu-id="ff8a0-156">After you have installed an application proxy connector within your environment, it can be easily configured with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-156">After you have installed an application proxy connector within your environment, it can be easily configured with Azure AD.</span></span>

### <a name="integrating-custom-applications"></a><span data-ttu-id="ff8a0-157">Integrating custom applications</span><span class="sxs-lookup"><span data-stu-id="ff8a0-157">Integrating custom applications</span></span>
<span data-ttu-id="ff8a0-158">If you are writing a new application and want to assist developers in leveraging the power Azure AD, see [Guiding developers](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-158">If you are writing a new application and want to assist developers in leveraging the power Azure AD, see [Guiding developers](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="ff8a0-159">If you want to add your custom application to the Azure Application Gallery, see [“Bring your own app” with Azure AD Self-Service SAML configuration](https://cloudblogs.microsoft.com/enterprisemobility/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-now-in-preview/).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-159">If you want to add your custom application to the Azure Application Gallery, see [“Bring your own app” with Azure AD Self-Service SAML configuration](https://cloudblogs.microsoft.com/enterprisemobility/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-now-in-preview/).</span></span>

## <a name="managing-access-to-applications"></a><span data-ttu-id="ff8a0-160">Managing access to applications</span><span class="sxs-lookup"><span data-stu-id="ff8a0-160">Managing access to applications</span></span>
<span data-ttu-id="ff8a0-161">The following articles describe ways you can manage access to applications once they have been integrated with Azure AD using Azure AD Connectors and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-161">The following articles describe ways you can manage access to applications once they have been integrated with Azure AD using Azure AD Connectors and Azure AD.</span></span>

* [<span data-ttu-id="ff8a0-162">Managing access to apps using Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff8a0-162">Managing access to apps using Azure AD</span></span>](what-is-access-management.md)
* [<span data-ttu-id="ff8a0-163">Automating with Azure AD Connectors</span><span class="sxs-lookup"><span data-stu-id="ff8a0-163">Automating with Azure AD Connectors</span></span>](user-provisioning.md)
* [<span data-ttu-id="ff8a0-164">Assigning users to an application</span><span class="sxs-lookup"><span data-stu-id="ff8a0-164">Assigning users to an application</span></span>](../active-directory-applications-guiding-developers-assigning-users.md)
* [<span data-ttu-id="ff8a0-165">Assigning groups to an application</span><span class="sxs-lookup"><span data-stu-id="ff8a0-165">Assigning groups to an application</span></span>](../active-directory-applications-guiding-developers-assigning-groups.md)
* [<span data-ttu-id="ff8a0-166">Sharing accounts</span><span class="sxs-lookup"><span data-stu-id="ff8a0-166">Sharing accounts</span></span>](../active-directory-sharing-accounts.md)

## <a name="next-steps"></a><span data-ttu-id="ff8a0-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff8a0-167">Next steps</span></span>
<span data-ttu-id="ff8a0-168">For in-depth information, you can download Azure Active Directory deployment plans from [GitHub](https://aka.ms/deploymentplans).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-168">For in-depth information, you can download Azure Active Directory deployment plans from [GitHub](https://aka.ms/deploymentplans).</span></span> <span data-ttu-id="ff8a0-169">For gallery applications, you can download deployment plans for single sign-on, conditional access, and user provisioning through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-169">For gallery applications, you can download deployment plans for single sign-on, conditional access, and user provisioning through the [Azure portal](https://portal.azure.com).</span></span> 

<span data-ttu-id="ff8a0-170">To download a deployment plan from the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="ff8a0-170">To download a deployment plan from the Azure portal:</span></span>

1. <span data-ttu-id="ff8a0-171">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-171">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ff8a0-172">Select **Enterprise Applications** | **Pick an App** | **Deployment Plan**.</span><span class="sxs-lookup"><span data-stu-id="ff8a0-172">Select **Enterprise Applications** | **Pick an App** | **Deployment Plan**.</span></span>

<span data-ttu-id="ff8a0-173">Please provide feedback on deployment plans by taking the [Deployment plan survey](https://aka.ms/DeploymentPlanFeedback).</span><span class="sxs-lookup"><span data-stu-id="ff8a0-173">Please provide feedback on deployment plans by taking the [Deployment plan survey](https://aka.ms/DeploymentPlanFeedback).</span></span>
