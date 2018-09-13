---
title: Develop apps for Azure AD | Microsoft Docs'
description: Written for the IT Pro, this article provides guidelines for integrating Azure applications with Active Directory.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: aa3c83f82d1a60253f70350e88aa96fb285ef3d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551469"
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="1e852-103">Develop line-of-business apps for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e852-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="1e852-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span><span class="sxs-lookup"><span data-stu-id="1e852-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="1e852-105">Overview</span><span class="sxs-lookup"><span data-stu-id="1e852-105">Overview</span></span>
<span data-ttu-id="1e852-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span><span class="sxs-lookup"><span data-stu-id="1e852-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="1e852-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span><span class="sxs-lookup"><span data-stu-id="1e852-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="1e852-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1e852-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="1e852-109">Register your application to use Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e852-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="1e852-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span><span class="sxs-lookup"><span data-stu-id="1e852-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="1e852-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span><span class="sxs-lookup"><span data-stu-id="1e852-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="1e852-112">Registering an application allows any user to do the following:</span><span class="sxs-lookup"><span data-stu-id="1e852-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="1e852-113">Get an identity for their application that Azure AD recognizes</span><span class="sxs-lookup"><span data-stu-id="1e852-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="1e852-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span><span class="sxs-lookup"><span data-stu-id="1e852-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="1e852-115">Brand the application in the Azure portal with a custom name, logo, etc.</span><span class="sxs-lookup"><span data-stu-id="1e852-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="1e852-116">Apply Azure AD authorization features to their app, including:</span><span class="sxs-lookup"><span data-stu-id="1e852-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="1e852-117">Role-Based Access Control (RBAC)</span><span class="sxs-lookup"><span data-stu-id="1e852-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="1e852-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span><span class="sxs-lookup"><span data-stu-id="1e852-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="1e852-119">Declare required permissions necessary for the application to function as expected, including:</span><span class="sxs-lookup"><span data-stu-id="1e852-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="1e852-120">App permissions (global administrators only).</span><span class="sxs-lookup"><span data-stu-id="1e852-120">App permissions (global administrators only).</span></span> <span data-ttu-id="1e852-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span><span class="sxs-lookup"><span data-stu-id="1e852-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="1e852-122">Delegated permissions (any user).</span><span class="sxs-lookup"><span data-stu-id="1e852-122">Delegated permissions (any user).</span></span> <span data-ttu-id="1e852-123">For example: Azure AD, Sign-in, and Read Profile</span><span class="sxs-lookup"><span data-stu-id="1e852-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="1e852-124">By default, any member can register an application.</span><span class="sxs-lookup"><span data-stu-id="1e852-124">By default, any member can register an application.</span></span> <span data-ttu-id="1e852-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="1e852-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="1e852-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span><span class="sxs-lookup"><span data-stu-id="1e852-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="1e852-127">Configure access rules (access policy/MFA)</span><span class="sxs-lookup"><span data-stu-id="1e852-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="1e852-128">Configure the app to require user assignment and assign users</span><span class="sxs-lookup"><span data-stu-id="1e852-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="1e852-129">Suppress the default user consent experience</span><span class="sxs-lookup"><span data-stu-id="1e852-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="1e852-130">Configure access rules</span><span class="sxs-lookup"><span data-stu-id="1e852-130">Configure access rules</span></span>
<span data-ttu-id="1e852-131">Configure per-application access rules to your SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1e852-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="1e852-132">For example, you can require MFA or only allow access to users on trusted networks.</span><span class="sxs-lookup"><span data-stu-id="1e852-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="1e852-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1e852-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="1e852-134">Configure the app to require user assignment and assign users</span><span class="sxs-lookup"><span data-stu-id="1e852-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="1e852-135">By default, users can access applications without being assigned.</span><span class="sxs-lookup"><span data-stu-id="1e852-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="1e852-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span><span class="sxs-lookup"><span data-stu-id="1e852-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="1e852-137">Requiring user assignment</span><span class="sxs-lookup"><span data-stu-id="1e852-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="1e852-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span><span class="sxs-lookup"><span data-stu-id="1e852-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="1e852-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span><span class="sxs-lookup"><span data-stu-id="1e852-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="1e852-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span><span class="sxs-lookup"><span data-stu-id="1e852-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="1e852-141">Assigning users to an application</span><span class="sxs-lookup"><span data-stu-id="1e852-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="1e852-142">Assigning groups to an application</span><span class="sxs-lookup"><span data-stu-id="1e852-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="1e852-143">Suppress user consent</span><span class="sxs-lookup"><span data-stu-id="1e852-143">Suppress user consent</span></span>
<span data-ttu-id="1e852-144">By default, each user goes through a consent experience to sign in.</span><span class="sxs-lookup"><span data-stu-id="1e852-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="1e852-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span><span class="sxs-lookup"><span data-stu-id="1e852-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="1e852-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span><span class="sxs-lookup"><span data-stu-id="1e852-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="1e852-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="1e852-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="1e852-148">Related Articles</span><span class="sxs-lookup"><span data-stu-id="1e852-148">Related Articles</span></span>
* [<span data-ttu-id="1e852-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="1e852-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="1e852-150">Azure Conditional Access Preview for SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="1e852-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="1e852-151">Managing access to apps with Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e852-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="1e852-152">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e852-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
