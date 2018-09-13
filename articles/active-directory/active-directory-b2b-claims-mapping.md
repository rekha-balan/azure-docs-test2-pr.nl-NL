---
title: B2B collaboration user claims mapping in Azure Active Directory | Microsoft Docs
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: e9fe8ebce7e4fe604d86308ad72092fd512d2662
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548948"
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="6592b-103">B2B collaboration user claims mapping in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6592b-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="6592b-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span><span class="sxs-lookup"><span data-stu-id="6592b-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="6592b-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span><span class="sxs-lookup"><span data-stu-id="6592b-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="6592b-106">By default, this includes the user's user name, email address, first name, and last name.</span><span class="sxs-lookup"><span data-stu-id="6592b-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="6592b-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span><span class="sxs-lookup"><span data-stu-id="6592b-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="6592b-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span><span class="sxs-lookup"><span data-stu-id="6592b-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="6592b-109">The application has been written to require a different set of claim URIs or claim values</span><span class="sxs-lookup"><span data-stu-id="6592b-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="6592b-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6592b-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![view claims in SAML token](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="6592b-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="6592b-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="6592b-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span><span class="sxs-lookup"><span data-stu-id="6592b-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6592b-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="6592b-114">Next steps</span></span>

<span data-ttu-id="6592b-115">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="6592b-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6592b-116">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="6592b-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6592b-117">B2B collaboration user properties</span><span class="sxs-lookup"><span data-stu-id="6592b-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="6592b-118">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="6592b-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="6592b-119">Delegate B2bB collaboration invitations</span><span class="sxs-lookup"><span data-stu-id="6592b-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="6592b-120">Dynamic groups and B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="6592b-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="6592b-121">B2B collaboration code and PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="6592b-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="6592b-122">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="6592b-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="6592b-123">Office 365 external sharing</span><span class="sxs-lookup"><span data-stu-id="6592b-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="6592b-124">B2B collaboration user tokens</span><span class="sxs-lookup"><span data-stu-id="6592b-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="6592b-125">B2B collaboration current limitations</span><span class="sxs-lookup"><span data-stu-id="6592b-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

