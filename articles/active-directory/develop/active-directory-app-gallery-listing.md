---
title: Listing your application in the Azure Active Directory application gallery
description: How to list an application that supports single sign-on in the Azure Active Directory gallery | Microsoft Azure
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/07/2017
ms.author: mbaldwin
ms.openlocfilehash: df60c4737954e79ff860601412dffa58d4dbb471
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669471"
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="c45f8-103">Listing your application in the Azure Active Directory application gallery</span><span class="sxs-lookup"><span data-stu-id="c45f8-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="c45f8-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span><span class="sxs-lookup"><span data-stu-id="c45f8-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="c45f8-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span><span class="sxs-lookup"><span data-stu-id="c45f8-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="c45f8-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span><span class="sxs-lookup"><span data-stu-id="c45f8-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="c45f8-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="c45f8-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="c45f8-108">Listing requirements for each mode are below.</span><span class="sxs-lookup"><span data-stu-id="c45f8-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="c45f8-109">OpenID Connect Integration</span><span class="sxs-lookup"><span data-stu-id="c45f8-109">OpenID Connect Integration</span></span>
<span data-ttu-id="c45f8-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="c45f8-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="c45f8-111">Then complete the questions below and send to waadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c45f8-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="c45f8-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span><span class="sxs-lookup"><span data-stu-id="c45f8-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="c45f8-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="c45f8-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="c45f8-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span><span class="sxs-lookup"><span data-stu-id="c45f8-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="c45f8-115">Provide the info below:</span><span class="sxs-lookup"><span data-stu-id="c45f8-115">Provide the info below:</span></span>

> <span data-ttu-id="c45f8-116">Company Name:</span><span class="sxs-lookup"><span data-stu-id="c45f8-116">Company Name:</span></span>
> 
> <span data-ttu-id="c45f8-117">Company Website:</span><span class="sxs-lookup"><span data-stu-id="c45f8-117">Company Website:</span></span>
> 
> <span data-ttu-id="c45f8-118">Application Name:</span><span class="sxs-lookup"><span data-stu-id="c45f8-118">Application Name:</span></span>
> 
> <span data-ttu-id="c45f8-119">Application Description (256 character limit):</span><span class="sxs-lookup"><span data-stu-id="c45f8-119">Application Description (256 character limit):</span></span>
> 
> <span data-ttu-id="c45f8-120">Application Website (informational):</span><span class="sxs-lookup"><span data-stu-id="c45f8-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="c45f8-121">Application Technical Support Website or Contact Info:</span><span class="sxs-lookup"><span data-stu-id="c45f8-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="c45f8-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="c45f8-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="c45f8-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span><span class="sxs-lookup"><span data-stu-id="c45f8-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="c45f8-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="c45f8-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="c45f8-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span><span class="sxs-lookup"><span data-stu-id="c45f8-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="c45f8-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span><span class="sxs-lookup"><span data-stu-id="c45f8-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="c45f8-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span><span class="sxs-lookup"><span data-stu-id="c45f8-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="c45f8-128">SAML Integration</span><span class="sxs-lookup"><span data-stu-id="c45f8-128">SAML Integration</span></span>
<span data-ttu-id="c45f8-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c45f8-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="c45f8-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="c45f8-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="c45f8-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span><span class="sxs-lookup"><span data-stu-id="c45f8-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="c45f8-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c45f8-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="c45f8-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span><span class="sxs-lookup"><span data-stu-id="c45f8-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="c45f8-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="c45f8-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="c45f8-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span><span class="sxs-lookup"><span data-stu-id="c45f8-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="c45f8-136">Provide the info below:</span><span class="sxs-lookup"><span data-stu-id="c45f8-136">Provide the info below:</span></span>

> <span data-ttu-id="c45f8-137">Company Name:</span><span class="sxs-lookup"><span data-stu-id="c45f8-137">Company Name:</span></span>
> 
> <span data-ttu-id="c45f8-138">Company Website:</span><span class="sxs-lookup"><span data-stu-id="c45f8-138">Company Website:</span></span>
> 
> <span data-ttu-id="c45f8-139">Application Name:</span><span class="sxs-lookup"><span data-stu-id="c45f8-139">Application Name:</span></span>
> 
> <span data-ttu-id="c45f8-140">Application Description (256 character limit):</span><span class="sxs-lookup"><span data-stu-id="c45f8-140">Application Description (256 character limit):</span></span>
> 
> <span data-ttu-id="c45f8-141">Application Website (informational):</span><span class="sxs-lookup"><span data-stu-id="c45f8-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="c45f8-142">Application Technical Support Website or Contact Info:</span><span class="sxs-lookup"><span data-stu-id="c45f8-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="c45f8-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span><span class="sxs-lookup"><span data-stu-id="c45f8-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="c45f8-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="c45f8-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="c45f8-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span><span class="sxs-lookup"><span data-stu-id="c45f8-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="c45f8-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span><span class="sxs-lookup"><span data-stu-id="c45f8-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="c45f8-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span><span class="sxs-lookup"><span data-stu-id="c45f8-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

