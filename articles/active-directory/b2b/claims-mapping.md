---
title: B2B collaboration user claims mapping in Azure Active Directory | Microsoft Docs
description: Customize the user claims that are issued in the SAML token for Azure Active Directory (Azure AD) B2B users.
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 04/06/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 50dccd91b35fabae4f54c361eedf4c98dbd4995c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870236"
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="fbc9e-103">B2B collaboration user claims mapping in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbc9e-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="fbc9e-104">Azure Active Directory (Azure AD) supports customizing the claims that are issued in the SAML token for B2B collaboration users.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-104">Azure Active Directory (Azure AD) supports customizing the claims that are issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="fbc9e-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="fbc9e-106">By default, this includes the user's user name, email address, first name, and last name.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-106">By default, this includes the user's user name, email address, first name, and last name.</span></span>

<span data-ttu-id="fbc9e-107">In the [Azure portal](https://portal.azure.com), you can view or edit the claims that are sent in the SAML token to the application.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-107">In the [Azure portal](https://portal.azure.com), you can view or edit the claims that are sent in the SAML token to the application.</span></span> <span data-ttu-id="fbc9e-108">To access the settings, select **Azure Active Directory** > **Enterprise applications** > the application that's configured for single sign-on > **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-108">To access the settings, select **Azure Active Directory** > **Enterprise applications** > the application that's configured for single sign-on > **Single sign-on**.</span></span> <span data-ttu-id="fbc9e-109">See the SAML token settings in the **User Attributes** section.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-109">See the SAML token settings in the **User Attributes** section.</span></span>

![Shows the SAML token attributes in the UI](media/claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="fbc9e-111">There are two possible reasons why you might need to edit the claims that are issued in the SAML token:</span><span class="sxs-lookup"><span data-stu-id="fbc9e-111">There are two possible reasons why you might need to edit the claims that are issued in the SAML token:</span></span>

1. <span data-ttu-id="fbc9e-112">The application requires a different set of claim URIs or claim values.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-112">The application requires a different set of claim URIs or claim values.</span></span>

2. <span data-ttu-id="fbc9e-113">The application requires the NameIdentifier claim to be something other than the user principal name (UPN) that's stored in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-113">The application requires the NameIdentifier claim to be something other than the user principal name (UPN) that's stored in Azure AD.</span></span>

<span data-ttu-id="fbc9e-114">For information about how to add and edit claims, see [Customizing claims issued in the SAML token for enterprise applications in Azure Active Directory](../develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9e-114">For information about how to add and edit claims, see [Customizing claims issued in the SAML token for enterprise applications in Azure Active Directory](../develop/active-directory-saml-claims-customization.md).</span></span>

<span data-ttu-id="fbc9e-115">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span><span class="sxs-lookup"><span data-stu-id="fbc9e-115">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbc9e-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbc9e-116">Next steps</span></span>

- <span data-ttu-id="fbc9e-117">For information about B2B collaboration user properties, see [Properties of an Azure Active Directory B2B collaboration user](user-properties.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9e-117">For information about B2B collaboration user properties, see [Properties of an Azure Active Directory B2B collaboration user](user-properties.md).</span></span>
- <span data-ttu-id="fbc9e-118">For information about user tokens for B2B collaboration users, see [Understand user tokens in Azure AD B2B collaboration](user-token.md).</span><span class="sxs-lookup"><span data-stu-id="fbc9e-118">For information about user tokens for B2B collaboration users, see [Understand user tokens in Azure AD B2B collaboration](user-token.md).</span></span>

