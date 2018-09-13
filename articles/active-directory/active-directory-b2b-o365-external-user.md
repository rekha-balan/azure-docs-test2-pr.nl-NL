---
title: Office 365 external sharing and Azure Active Directory B2B collaboration | Microsoft Docs
description: claims mapping reference for Azure Active Directory B2B collaboration
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
ms.date: 02/06/2017
ms.author: sasubram
ms.openlocfilehash: 2cad06d665611c50b135892333fbb34974731c76
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555091"
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="7405a-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="7405a-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="7405a-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) business-to-business (B2B) collaboration are technically the same thing.</span><span class="sxs-lookup"><span data-stu-id="7405a-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) business-to-business (B2B) collaboration are technically the same thing.</span></span> <span data-ttu-id="7405a-105">All external sharing (except OneDrive/SharePoint Online), including Guests in Unified Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span><span class="sxs-lookup"><span data-stu-id="7405a-105">All external sharing (except OneDrive/SharePoint Online), including Guests in Unified Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="7405a-106">OneDrive/SharePoint Online has a separate invitation manager.</span><span class="sxs-lookup"><span data-stu-id="7405a-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="7405a-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span><span class="sxs-lookup"><span data-stu-id="7405a-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="7405a-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span><span class="sxs-lookup"><span data-stu-id="7405a-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="7405a-109">We are working with OneDrive/SharePoint Online to add the Azure AD B2B invitation APIs (referred to in this documentation) to unify the process across products and adopt all the innovations that Azure AD is making.</span><span class="sxs-lookup"><span data-stu-id="7405a-109">We are working with OneDrive/SharePoint Online to add the Azure AD B2B invitation APIs (referred to in this documentation) to unify the process across products and adopt all the innovations that Azure AD is making.</span></span> <span data-ttu-id="7405a-110">In the meantime, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span><span class="sxs-lookup"><span data-stu-id="7405a-110">In the meantime, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="7405a-111">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span><span class="sxs-lookup"><span data-stu-id="7405a-111">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="7405a-112">So, before redemption, you don't see the user in Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="7405a-112">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="7405a-113">If another site invites a user in the meantime, a new invitation is generated.</span><span class="sxs-lookup"><span data-stu-id="7405a-113">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="7405a-114">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span><span class="sxs-lookup"><span data-stu-id="7405a-114">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="7405a-115">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span><span class="sxs-lookup"><span data-stu-id="7405a-115">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="7405a-116">After a user redeems an invitation, the experiences look alike.</span><span class="sxs-lookup"><span data-stu-id="7405a-116">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="7405a-117">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span><span class="sxs-lookup"><span data-stu-id="7405a-117">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="7405a-118">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span><span class="sxs-lookup"><span data-stu-id="7405a-118">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="7405a-119">To use external sharing in OneDrive/SharePoint Online together with Azure AD B2B collaboration in a managed, admin-controlled way, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span><span class="sxs-lookup"><span data-stu-id="7405a-119">To use external sharing in OneDrive/SharePoint Online together with Azure AD B2B collaboration in a managed, admin-controlled way, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="7405a-120">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span><span class="sxs-lookup"><span data-stu-id="7405a-120">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="7405a-121">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span><span class="sxs-lookup"><span data-stu-id="7405a-121">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![The OneDrive/SharePoint Online external sharing setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="7405a-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="7405a-123">Next steps</span></span>

<span data-ttu-id="7405a-124">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="7405a-124">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="7405a-125">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="7405a-125">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="7405a-126">B2B collaboration user properties</span><span class="sxs-lookup"><span data-stu-id="7405a-126">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="7405a-127">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="7405a-127">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="7405a-128">Delegate B2B collaboration invitations</span><span class="sxs-lookup"><span data-stu-id="7405a-128">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="7405a-129">Dynamic groups and B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="7405a-129">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="7405a-130">B2B collaboration code and PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="7405a-130">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="7405a-131">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="7405a-131">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="7405a-132">B2B collaboration user tokens</span><span class="sxs-lookup"><span data-stu-id="7405a-132">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="7405a-133">B2B collaboration user claims mapping</span><span class="sxs-lookup"><span data-stu-id="7405a-133">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="7405a-134">B2B collaboration current limitations</span><span class="sxs-lookup"><span data-stu-id="7405a-134">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

