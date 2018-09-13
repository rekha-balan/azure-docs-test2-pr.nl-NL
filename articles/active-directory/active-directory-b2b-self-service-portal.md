---
title: Self-service sign-up portal for Azure Active Directory B2B collaboration | Microsoft Docs
description: Azure Active Directory B2B collaboration supports your cross-company relationships by enabling business partners to selectively access your corporate applications
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: f629eeb6f12c8785cab2585190f70e98b02fa5b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555936"
---
# <a name="self-service-sign-up-portal-for-azure-ad-b2b-collaboration"></a><span data-ttu-id="40a09-103">Self-service sign-up portal for Azure AD B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="40a09-103">Self-service sign-up portal for Azure AD B2B collaboration</span></span>

<span data-ttu-id="40a09-104">Customers can do a lot with the built-in product capabilities that are exposed through our IT admin experiences in the [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for non-admins.</span><span class="sxs-lookup"><span data-stu-id="40a09-104">Customers can do a lot with the built-in product capabilities that are exposed through our IT admin experiences in the [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for non-admins.</span></span> <span data-ttu-id="40a09-105">But we are also aware that businesses need to customize the onboarding workflow for B2B users to fit their organization’s needs.</span><span class="sxs-lookup"><span data-stu-id="40a09-105">But we are also aware that businesses need to customize the onboarding workflow for B2B users to fit their organization’s needs.</span></span> <span data-ttu-id="40a09-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="40a09-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="40a09-107">In discussing this with many of our customers, we saw one common need rise up above all others.</span><span class="sxs-lookup"><span data-stu-id="40a09-107">In discussing this with many of our customers, we saw one common need rise up above all others.</span></span> <span data-ttu-id="40a09-108">This was the case where the inviting organization may not know (or want to know) ahead of time who the individual external collaborators are that needed access to their resources.</span><span class="sxs-lookup"><span data-stu-id="40a09-108">This was the case where the inviting organization may not know (or want to know) ahead of time who the individual external collaborators are that needed access to their resources.</span></span> <span data-ttu-id="40a09-109">They wanted a way where users from partner companies can self-sign-up with a set of policies that the inviting organization controlled.</span><span class="sxs-lookup"><span data-stu-id="40a09-109">They wanted a way where users from partner companies can self-sign-up with a set of policies that the inviting organization controlled.</span></span> <span data-ttu-id="40a09-110">This is possible through our APIs – so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="40a09-110">This is possible through our APIs – so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="40a09-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy based, self-service sign-up capability for their trusted partners, with rules that determine which apps they should get access to.</span><span class="sxs-lookup"><span data-stu-id="40a09-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy based, self-service sign-up capability for their trusted partners, with rules that determine which apps they should get access to.</span></span> <span data-ttu-id="40a09-112">This way, partner users can get access to the right resources when they need it, securely, but without anyone in the inviting organization having to manually onboard them.</span><span class="sxs-lookup"><span data-stu-id="40a09-112">This way, partner users can get access to the right resources when they need it, securely, but without anyone in the inviting organization having to manually onboard them.</span></span> <span data-ttu-id="40a09-113">You can easily deploy the project with a click of a button into an Azure subscription of your choice.</span><span class="sxs-lookup"><span data-stu-id="40a09-113">You can easily deploy the project with a click of a button into an Azure subscription of your choice.</span></span> <span data-ttu-id="40a09-114">Give it a whirl!</span><span class="sxs-lookup"><span data-stu-id="40a09-114">Give it a whirl!</span></span>

## <a name="as-is-code"></a><span data-ttu-id="40a09-115">As-is code</span><span class="sxs-lookup"><span data-stu-id="40a09-115">As-is code</span></span>

<span data-ttu-id="40a09-116">Remember that this code is made available as a sample to demonstrate usage of the Azure Active Directory B2B Invitation API.</span><span class="sxs-lookup"><span data-stu-id="40a09-116">Remember that this code is made available as a sample to demonstrate usage of the Azure Active Directory B2B Invitation API.</span></span> <span data-ttu-id="40a09-117">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span><span class="sxs-lookup"><span data-stu-id="40a09-117">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40a09-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="40a09-118">Next steps</span></span>

<span data-ttu-id="40a09-119">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="40a09-119">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="40a09-120">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="40a09-120">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="40a09-121">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="40a09-121">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="40a09-122">How do information workers add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="40a09-122">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="40a09-123">The elements of the B2B collaboration invitation email</span><span class="sxs-lookup"><span data-stu-id="40a09-123">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="40a09-124">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="40a09-124">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="40a09-125">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="40a09-125">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="40a09-126">Troubleshooting Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="40a09-126">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="40a09-127">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="40a09-127">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="40a09-128">Multi-factor authentication for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="40a09-128">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="40a09-129">Add B2B collaboration users without an invitation</span><span class="sxs-lookup"><span data-stu-id="40a09-129">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="40a09-130">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40a09-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)