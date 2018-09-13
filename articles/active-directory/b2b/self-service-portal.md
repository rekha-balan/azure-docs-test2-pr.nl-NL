---
title: Self-service sign-up portal for Azure Active Directory B2B collaboration | Microsoft Docs
description: Azure Active Directory B2B collaboration supports your cross-company relationships by enabling business partners to selectively access your corporate applications
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 05/08/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 94001b005a883c172cab279029b47ac1ad0c0de5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969194"
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="65e59-103">Self-service portal for Azure AD B2B collaboration sign-up</span><span class="sxs-lookup"><span data-stu-id="65e59-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="65e59-104">Customers can do a lot with the built-in features that are exposed through the [Azure portal](https://portal.azure.com) and the [Application Access Panel](https://myapps.microsoft.com) for end users.</span><span class="sxs-lookup"><span data-stu-id="65e59-104">Customers can do a lot with the built-in features that are exposed through the [Azure portal](https://portal.azure.com) and the [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="65e59-105">However, you might need to customize the onboarding workflow for B2B users to fit your organization’s needs.</span><span class="sxs-lookup"><span data-stu-id="65e59-105">However, you might need to customize the onboarding workflow for B2B users to fit your organization’s needs.</span></span> <span data-ttu-id="65e59-106">You can do that with [the invitation API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="65e59-106">You can do that with [the invitation API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="65e59-107">As an inviting organization, you may not know ahead of time who the individual external collaborators are who need access to your resources.</span><span class="sxs-lookup"><span data-stu-id="65e59-107">As an inviting organization, you may not know ahead of time who the individual external collaborators are who need access to your resources.</span></span> <span data-ttu-id="65e59-108">You need a way for users from partner companies to sign themselves up with a set of policies that you as the inviting organization controls.</span><span class="sxs-lookup"><span data-stu-id="65e59-108">You need a way for users from partner companies to sign themselves up with a set of policies that you as the inviting organization controls.</span></span> <span data-ttu-id="65e59-109">This scenario is possible through the APIs.</span><span class="sxs-lookup"><span data-stu-id="65e59-109">This scenario is possible through the APIs.</span></span> <span data-ttu-id="65e59-110">There's a [sample project on GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) that does just that.</span><span class="sxs-lookup"><span data-stu-id="65e59-110">There's a [sample project on GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) that does just that.</span></span>

<span data-ttu-id="65e59-111">This GitHub project shows how organizations can use the APIs to provide a policy-based, self-service sign-up capability for your trusted partners, with rules that determine the apps they can access.</span><span class="sxs-lookup"><span data-stu-id="65e59-111">This GitHub project shows how organizations can use the APIs to provide a policy-based, self-service sign-up capability for your trusted partners, with rules that determine the apps they can access.</span></span> <span data-ttu-id="65e59-112">Partner users can get access to resources when they need them.</span><span class="sxs-lookup"><span data-stu-id="65e59-112">Partner users can get access to resources when they need them.</span></span> <span data-ttu-id="65e59-113">They can do this securely, without requiring the inviting organization to manually onboard them.</span><span class="sxs-lookup"><span data-stu-id="65e59-113">They can do this securely, without requiring the inviting organization to manually onboard them.</span></span> <span data-ttu-id="65e59-114">You can easily deploy the project into an Azure subscription of your choice.</span><span class="sxs-lookup"><span data-stu-id="65e59-114">You can easily deploy the project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="65e59-115">As-is code</span><span class="sxs-lookup"><span data-stu-id="65e59-115">As-is code</span></span>

<span data-ttu-id="65e59-116">This code is made available as a sample to demonstrate usage of the Azure Active Directory B2B invitation API.</span><span class="sxs-lookup"><span data-stu-id="65e59-116">This code is made available as a sample to demonstrate usage of the Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="65e59-117">It should be customized by your development team or a partner, and should be reviewed before you deploy it in a production scenario.</span><span class="sxs-lookup"><span data-stu-id="65e59-117">It should be customized by your development team or a partner, and should be reviewed before you deploy it in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65e59-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="65e59-118">Next steps</span></span>

* [<span data-ttu-id="65e59-119">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="65e59-119">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
* [<span data-ttu-id="65e59-120">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="65e59-120">Azure AD B2B collaboration licensing</span></span>](licensing-guidance.md)
* [<span data-ttu-id="65e59-121">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="65e59-121">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](faq.md)