---
title: Enable a trial in the Azure Marketplace by using Azure Active Directory | Azure
description: Enable a Trial listing type by using Azure Active Directory in the Azure Marketplace and AppSource for app and service publishers.
services: Azure, Marketplace, Compute, Storage, Networking, Blockchain, Security
documentationcenter: ''
author: jm-aditi-ms
manager: pabutler
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 06/04/2018
ms.author: ellacroi
ms.openlocfilehash: c5b7b4967c1acef733d366e651d50706db42aace
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868430"
---
# <a name="enable-a-trial-listing-by-using-azure-active-directory"></a><span data-ttu-id="816f1-103">Enable a trial listing by using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="816f1-103">Enable a trial listing by using Azure Active Directory</span></span>

<span data-ttu-id="816f1-104">Azure Active Directory (Azure AD) is a cloud identity service that enables authentication with a Microsoft work or school account by using industry-standard frameworks.</span><span class="sxs-lookup"><span data-stu-id="816f1-104">Azure Active Directory (Azure AD) is a cloud identity service that enables authentication with a Microsoft work or school account by using industry-standard frameworks.</span></span> <span data-ttu-id="816f1-105">Azure AD supports OAuth and OpenID Connect authentication.</span><span class="sxs-lookup"><span data-stu-id="816f1-105">Azure AD supports OAuth and OpenID Connect authentication.</span></span> <span data-ttu-id="816f1-106">The [Azure Marketplace](https://azuremarketplace.microsoft.com) uses Azure AD to authenticate you and your customers.</span><span class="sxs-lookup"><span data-stu-id="816f1-106">The [Azure Marketplace](https://azuremarketplace.microsoft.com) uses Azure AD to authenticate you and your customers.</span></span>

<span data-ttu-id="816f1-107">For more information about Azure AD, see [Azure Active Directory](https://azure.microsoft.com/services/active-directory).</span><span class="sxs-lookup"><span data-stu-id="816f1-107">For more information about Azure AD, see [Azure Active Directory](https://azure.microsoft.com/services/active-directory).</span></span>

<span data-ttu-id="816f1-108">After a customer selects your trial listing in the Marketplace, your customer is redirected to your trial environment.</span><span class="sxs-lookup"><span data-stu-id="816f1-108">After a customer selects your trial listing in the Marketplace, your customer is redirected to your trial environment.</span></span> <span data-ttu-id="816f1-109">In your trial environment, you can set up your customer directly without requiring additional sign-in steps.</span><span class="sxs-lookup"><span data-stu-id="816f1-109">In your trial environment, you can set up your customer directly without requiring additional sign-in steps.</span></span> <span data-ttu-id="816f1-110">Your app or offer receives a token from Azure AD during authentication.</span><span class="sxs-lookup"><span data-stu-id="816f1-110">Your app or offer receives a token from Azure AD during authentication.</span></span> <span data-ttu-id="816f1-111">The token includes valuable user information that's used to create a user account in your app or offer.</span><span class="sxs-lookup"><span data-stu-id="816f1-111">The token includes valuable user information that's used to create a user account in your app or offer.</span></span> <span data-ttu-id="816f1-112">You can automate customer setup and increase the likelihood of conversion.</span><span class="sxs-lookup"><span data-stu-id="816f1-112">You can automate customer setup and increase the likelihood of conversion.</span></span>

<span data-ttu-id="816f1-113">For more information about the token that's sent from Azure AD during authentication, see [Sample tokens](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims#sample-tokens).</span><span class="sxs-lookup"><span data-stu-id="816f1-113">For more information about the token that's sent from Azure AD during authentication, see [Sample tokens](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims#sample-tokens).</span></span>

<span data-ttu-id="816f1-114">Use Azure AD to enable one-click authentication in your app or trial.</span><span class="sxs-lookup"><span data-stu-id="816f1-114">Use Azure AD to enable one-click authentication in your app or trial.</span></span> <span data-ttu-id="816f1-115">Azure AD gives you the following benefits:</span><span class="sxs-lookup"><span data-stu-id="816f1-115">Azure AD gives you the following benefits:</span></span> 
*   <span data-ttu-id="816f1-116">Streamline the customer experience from the Marketplace to trial.</span><span class="sxs-lookup"><span data-stu-id="816f1-116">Streamline the customer experience from the Marketplace to trial.</span></span>
*   <span data-ttu-id="816f1-117">Maintain the feel of an in-product experience, even when the user is redirected from the Marketplace to your domain or trial environment.</span><span class="sxs-lookup"><span data-stu-id="816f1-117">Maintain the feel of an in-product experience, even when the user is redirected from the Marketplace to your domain or trial environment.</span></span>
*   <span data-ttu-id="816f1-118">Reduce the likelihood of abandonment upon redirect, because there are no additional sign-in steps.</span><span class="sxs-lookup"><span data-stu-id="816f1-118">Reduce the likelihood of abandonment upon redirect, because there are no additional sign-in steps.</span></span>
*   <span data-ttu-id="816f1-119">Reduce deployment barriers for the large population of Azure AD users.</span><span class="sxs-lookup"><span data-stu-id="816f1-119">Reduce deployment barriers for the large population of Azure AD users.</span></span>

## <a name="verify-your-azure-ad-integration-in-the-marketplace-multitenant-apps"></a><span data-ttu-id="816f1-120">Verify your Azure AD integration in the Marketplace: Multitenant apps</span><span class="sxs-lookup"><span data-stu-id="816f1-120">Verify your Azure AD integration in the Marketplace: Multitenant apps</span></span>
<span data-ttu-id="816f1-121">Use Azure AD to support the following options for your solution:</span><span class="sxs-lookup"><span data-stu-id="816f1-121">Use Azure AD to support the following options for your solution:</span></span>
*   <span data-ttu-id="816f1-122">Register your app in storefronts in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="816f1-122">Register your app in storefronts in the Marketplace.</span></span>
*   <span data-ttu-id="816f1-123">Enable the multitenancy support feature in Azure AD to get a one-click trial experience.</span><span class="sxs-lookup"><span data-stu-id="816f1-123">Enable the multitenancy support feature in Azure AD to get a one-click trial experience.</span></span>

<span data-ttu-id="816f1-124">For more information about app registration, see [Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).</span><span class="sxs-lookup"><span data-stu-id="816f1-124">For more information about app registration, see [Integrating applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).</span></span>

<span data-ttu-id="816f1-125">If you are new to using Azure AD federated single sign-on (SSO), complete these steps:</span><span class="sxs-lookup"><span data-stu-id="816f1-125">If you are new to using Azure AD federated single sign-on (SSO), complete these steps:</span></span>
1.  <span data-ttu-id="816f1-126">Register your app in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="816f1-126">Register your app in the Marketplace.</span></span> 
2.  <span data-ttu-id="816f1-127">Develop SSO with Azure AD by using OAuth 2.0 or OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="816f1-127">Develop SSO with Azure AD by using OAuth 2.0 or OpenID Connect.</span></span>
    *   <span data-ttu-id="816f1-128">For more information about OAuth 2.0, see [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code).</span><span class="sxs-lookup"><span data-stu-id="816f1-128">For more information about OAuth 2.0, see [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code).</span></span>
    *   <span data-ttu-id="816f1-129">For more information about Open ID Connect, see [OpenID Connect](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code).</span><span class="sxs-lookup"><span data-stu-id="816f1-129">For more information about Open ID Connect, see [OpenID Connect](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code).</span></span>
3.  <span data-ttu-id="816f1-130">Enable the multitenancy support feature in Azure AD to provide a one-click trial experience.</span><span class="sxs-lookup"><span data-stu-id="816f1-130">Enable the multitenancy support feature in Azure AD to provide a one-click trial experience.</span></span>
    
    <span data-ttu-id="816f1-131">For more information about AppSource certification, see [AppSource certification](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-appsource-certified).</span><span class="sxs-lookup"><span data-stu-id="816f1-131">For more information about AppSource certification, see [AppSource certification](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-appsource-certified).</span></span> 

## <a name="verify-your-azure-ad-integration-in-the-marketplace-single-tenant-apps"></a><span data-ttu-id="816f1-132">Verify your Azure AD integration in the Marketplace: Single-tenant apps</span><span class="sxs-lookup"><span data-stu-id="816f1-132">Verify your Azure AD integration in the Marketplace: Single-tenant apps</span></span>
<span data-ttu-id="816f1-133">Use Azure AD to support one of the following options for your single-tenant solution:</span><span class="sxs-lookup"><span data-stu-id="816f1-133">Use Azure AD to support one of the following options for your single-tenant solution:</span></span> 
*   <span data-ttu-id="816f1-134">Add users to your directory as guest users by using Azure Active Directory B2B (Azure AD B2B).</span><span class="sxs-lookup"><span data-stu-id="816f1-134">Add users to your directory as guest users by using Azure Active Directory B2B (Azure AD B2B).</span></span>
    
    <span data-ttu-id="816f1-135">For more information about Azure AD B2B, see [What is Azure AD B2B collaboration](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).</span><span class="sxs-lookup"><span data-stu-id="816f1-135">For more information about Azure AD B2B, see [What is Azure AD B2B collaboration](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).</span></span>
*   <span data-ttu-id="816f1-136">Manually set up trials for customers by using the Contact Me publishing option.</span><span class="sxs-lookup"><span data-stu-id="816f1-136">Manually set up trials for customers by using the Contact Me publishing option.</span></span>
*   <span data-ttu-id="816f1-137">Develop a per-customer test drive.</span><span class="sxs-lookup"><span data-stu-id="816f1-137">Develop a per-customer test drive.</span></span>
*   <span data-ttu-id="816f1-138">Build a multitenant sample demo app that uses SSO.</span><span class="sxs-lookup"><span data-stu-id="816f1-138">Build a multitenant sample demo app that uses SSO.</span></span>

## <a name="next-steps"></a><span data-ttu-id="816f1-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="816f1-139">Next steps</span></span>
*   <span data-ttu-id="816f1-140">Review the [Azure Marketplace and AppSource publishing guide](./marketplace-publishers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="816f1-140">Review the [Azure Marketplace and AppSource publishing guide](./marketplace-publishers-guide.md).</span></span>
