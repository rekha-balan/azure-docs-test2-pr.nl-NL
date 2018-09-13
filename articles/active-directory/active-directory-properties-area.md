---
title: Add your organization's privacy info in Azure AD | Microsoft Docs
description: Explains how to add your organization's privacy info to the Azure Active Directory (Azure AD) Properties area.
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: lizross
ms.reviewer: bpham
ms.custom: it-pro
ms.openlocfilehash: a34fa2b8c2d966af108664c219a222fb9a5b7abc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865183"
---
# <a name="how-to-add-your-organizations-privacy-info-in-azure-active-directory"></a><span data-ttu-id="42c55-103">How-to: Add your organization's privacy info in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42c55-103">How-to: Add your organization's privacy info in Azure Active Directory</span></span>
<span data-ttu-id="42c55-104">This article explains how a tenant admin can add privacy-related info to an organization’s Azure Active Directory (Azure AD) tenant, through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42c55-104">This article explains how a tenant admin can add privacy-related info to an organization’s Azure Active Directory (Azure AD) tenant, through the Azure portal.</span></span>

<span data-ttu-id="42c55-105">We strongly recommend you add both your global privacy contact and your organization’s privacy statement, so your internal employees and external guests can review your policies.</span><span class="sxs-lookup"><span data-stu-id="42c55-105">We strongly recommend you add both your global privacy contact and your organization’s privacy statement, so your internal employees and external guests can review your policies.</span></span> <span data-ttu-id="42c55-106">Because privacy statements are uniquely created and tailored for each business, we strongly recommend you contact a lawyer for assistance.</span><span class="sxs-lookup"><span data-stu-id="42c55-106">Because privacy statements are uniquely created and tailored for each business, we strongly recommend you contact a lawyer for assistance.</span></span>

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-dsr-and-stp-note.md)]

## <a name="access-the-properties-area-to-add-your-privacy-info"></a><span data-ttu-id="42c55-107">Access the Properties area to add your privacy info</span><span class="sxs-lookup"><span data-stu-id="42c55-107">Access the Properties area to add your privacy info</span></span>

1.  <span data-ttu-id="42c55-108">Sign in to the Azure portal as a tenant administrator.</span><span class="sxs-lookup"><span data-stu-id="42c55-108">Sign in to the Azure portal as a tenant administrator.</span></span>

2.  <span data-ttu-id="42c55-109">On the left navbar, select **Azure Active Directory**, and then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="42c55-109">On the left navbar, select **Azure Active Directory**, and then select **Properties**.</span></span>

    <span data-ttu-id="42c55-110">The **Properties** area appears.</span><span class="sxs-lookup"><span data-stu-id="42c55-110">The **Properties** area appears.</span></span>

    ![Azure AD Properties area highlighting the privacy info area](./media/active-directory-properties-area/properties-area.png)

3.  <span data-ttu-id="42c55-112">Add your privacy info for your employees:</span><span class="sxs-lookup"><span data-stu-id="42c55-112">Add your privacy info for your employees:</span></span>

    - <span data-ttu-id="42c55-113">**Technical contact.**</span><span class="sxs-lookup"><span data-stu-id="42c55-113">**Technical contact.**</span></span> <span data-ttu-id="42c55-114">Type the email address for the person to contact for technical support within your organization.</span><span class="sxs-lookup"><span data-stu-id="42c55-114">Type the email address for the person to contact for technical support within your organization.</span></span>
    
    - <span data-ttu-id="42c55-115">**Global privacy contact.**</span><span class="sxs-lookup"><span data-stu-id="42c55-115">**Global privacy contact.**</span></span> <span data-ttu-id="42c55-116">Type the email address for the person to contact for inquiries about personal data privacy.</span><span class="sxs-lookup"><span data-stu-id="42c55-116">Type the email address for the person to contact for inquiries about personal data privacy.</span></span> <span data-ttu-id="42c55-117">This person is also who Microsoft contacts if there's a data breach.</span><span class="sxs-lookup"><span data-stu-id="42c55-117">This person is also who Microsoft contacts if there's a data breach.</span></span> <span data-ttu-id="42c55-118">If there's no person listed here, Microsoft contacts your global administrators.</span><span class="sxs-lookup"><span data-stu-id="42c55-118">If there's no person listed here, Microsoft contacts your global administrators.</span></span>

    - <span data-ttu-id="42c55-119">**Privacy statement URL.**</span><span class="sxs-lookup"><span data-stu-id="42c55-119">**Privacy statement URL.**</span></span> <span data-ttu-id="42c55-120">Type the link to your organization’s document that describes how your organization handles both internal and external guest's data privacy.</span><span class="sxs-lookup"><span data-stu-id="42c55-120">Type the link to your organization’s document that describes how your organization handles both internal and external guest's data privacy.</span></span>

        >[!Important]
        ><span data-ttu-id="42c55-121">If you don’t include either your own privacy statement or your privacy contact, your external guests will see text in the **Review Permissions** box that says, **<_your org name_> has not provided links to their terms for you to review**.</span><span class="sxs-lookup"><span data-stu-id="42c55-121">If you don’t include either your own privacy statement or your privacy contact, your external guests will see text in the **Review Permissions** box that says, **<_your org name_> has not provided links to their terms for you to review**.</span></span> <span data-ttu-id="42c55-122">For example, a guest user will see this message when they receive an invitation to access an organization through B2B collaboration.</span><span class="sxs-lookup"><span data-stu-id="42c55-122">For example, a guest user will see this message when they receive an invitation to access an organization through B2B collaboration.</span></span>

        ![B2B Collaboration Review Permissions box with message](./media/active-directory-properties-area/active-directory-no-privacy-statement-or-contact.png)

4.  <span data-ttu-id="42c55-124">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="42c55-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42c55-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="42c55-125">Next steps</span></span>
- [<span data-ttu-id="42c55-126">Azure Active Directory B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="42c55-126">Azure Active Directory B2B collaboration invitation redemption</span></span>](https://aka.ms/b2bredemption)
- [<span data-ttu-id="42c55-127">Add or change profile information for a user in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42c55-127">Add or change profile information for a user in Azure Active Directory</span></span>](fundamentals/active-directory-users-profile-azure-portal.md)