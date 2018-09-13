---
title: 'Azure AD Connect: Features in preview | Microsoft Docs'
description: This topic describes in more detail features which are in preview in Azure AD Connect.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: billmath
ms.openlocfilehash: c1653c769a6b42d18ffb0da71220ce06c6556587
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550899"
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="01c9c-103">More details about features in preview</span><span class="sxs-lookup"><span data-stu-id="01c9c-103">More details about features in preview</span></span>
<span data-ttu-id="01c9c-104">This topic describes how to use features currently in preview.</span><span class="sxs-lookup"><span data-stu-id="01c9c-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="01c9c-105">Group writeback</span><span class="sxs-lookup"><span data-stu-id="01c9c-105">Group writeback</span></span>
<span data-ttu-id="01c9c-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span><span class="sxs-lookup"><span data-stu-id="01c9c-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="01c9c-107">This is a group that is always mastered in the cloud.</span><span class="sxs-lookup"><span data-stu-id="01c9c-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="01c9c-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span><span class="sxs-lookup"><span data-stu-id="01c9c-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="01c9c-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="01c9c-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="01c9c-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span><span class="sxs-lookup"><span data-stu-id="01c9c-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="01c9c-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span><span class="sxs-lookup"><span data-stu-id="01c9c-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="01c9c-112">**Notes during the preview**</span><span class="sxs-lookup"><span data-stu-id="01c9c-112">**Notes during the preview**</span></span>

* <span data-ttu-id="01c9c-113">The address book attribute is currently not populated in the preview.</span><span class="sxs-lookup"><span data-stu-id="01c9c-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="01c9c-114">Without this attribute, the group is not visible in the GAL.</span><span class="sxs-lookup"><span data-stu-id="01c9c-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="01c9c-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="01c9c-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="01c9c-116">Only forests with the Exchange schema are valid targets for groups.</span><span class="sxs-lookup"><span data-stu-id="01c9c-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="01c9c-117">If no Exchange was detected, then group writeback is not possible to enable.</span><span class="sxs-lookup"><span data-stu-id="01c9c-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="01c9c-118">Only single-forest Exchange organization deployments are currently supported.</span><span class="sxs-lookup"><span data-stu-id="01c9c-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="01c9c-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span><span class="sxs-lookup"><span data-stu-id="01c9c-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="01c9c-120">The Group writeback feature does not handle security groups or distribution groups.</span><span class="sxs-lookup"><span data-stu-id="01c9c-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="01c9c-121">A subscription to Azure AD Premium is required for group writeback.</span><span class="sxs-lookup"><span data-stu-id="01c9c-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="01c9c-122">User writeback</span><span class="sxs-lookup"><span data-stu-id="01c9c-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="01c9c-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="01c9c-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="01c9c-124">If you have enabled it, then you should disable this feature.</span><span class="sxs-lookup"><span data-stu-id="01c9c-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="01c9c-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="01c9c-125">Next steps</span></span>
<span data-ttu-id="01c9c-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="01c9c-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="01c9c-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="01c9c-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
