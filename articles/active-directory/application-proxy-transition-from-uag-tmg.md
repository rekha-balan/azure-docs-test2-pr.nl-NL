---
title: Transition to Azure AD application proxies from Microsoft Forefront | Microsoft Docs
description: Covers the basics about how to move from the Microsoft Forefront TMG and UAG solutions to Azure Active Directory application proxies.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: kgremban
ms.openlocfilehash: 542dd7df7e0b887298522f29cb597f1df73709cb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550290"
---
# <a name="transition-to-azure-ad-application-proxies-from-microsoft-forefront"></a><span data-ttu-id="85ce4-103">Transition to Azure AD application proxies from Microsoft Forefront</span><span class="sxs-lookup"><span data-stu-id="85ce4-103">Transition to Azure AD application proxies from Microsoft Forefront</span></span>

<span data-ttu-id="85ce4-104">This article describes how to move from the Microsoft Forefront Threat Management Gateway (TMG) and Unified Access Gateway (UAG) solutions to these Azure Active Directory (Azure AD) application proxies: Web Application Proxy and Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="85ce4-104">This article describes how to move from the Microsoft Forefront Threat Management Gateway (TMG) and Unified Access Gateway (UAG) solutions to these Azure Active Directory (Azure AD) application proxies: Web Application Proxy and Azure AD Application Proxy.</span></span>

> [!NOTE]
> <span data-ttu-id="85ce4-105">Azure AD Application Proxy is a feature that's available only if you upgraded to the Premium or Basic edition of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85ce4-105">Azure AD Application Proxy is a feature that's available only if you upgraded to the Premium or Basic edition of Azure AD.</span></span> <span data-ttu-id="85ce4-106">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="85ce4-106">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>


<span data-ttu-id="85ce4-107">For detailed information about the transition from Forefront TMG and UAG to the new application proxies, you can [download a related white paper from Microsoft](http://download.microsoft.com/download/3/E/3/3E335D93-6DB8-4834-90A8-B86105419F05/Microsoft%20TMG%20and%20UAG%20EOL%20and%20transitioning%20to%20WAP%20and%20AADAP.docx).</span><span class="sxs-lookup"><span data-stu-id="85ce4-107">For detailed information about the transition from Forefront TMG and UAG to the new application proxies, you can [download a related white paper from Microsoft](http://download.microsoft.com/download/3/E/3/3E335D93-6DB8-4834-90A8-B86105419F05/Microsoft%20TMG%20and%20UAG%20EOL%20and%20transitioning%20to%20WAP%20and%20AADAP.docx).</span></span>

## <a name="functionality-details-for-the-conversion"></a><span data-ttu-id="85ce4-108">Functionality details for the conversion</span><span class="sxs-lookup"><span data-stu-id="85ce4-108">Functionality details for the conversion</span></span>

|<span data-ttu-id="85ce4-109">**TMG/UAG functionality**</span><span class="sxs-lookup"><span data-stu-id="85ce4-109">**TMG/UAG functionality**</span></span>|<span data-ttu-id="85ce4-110">**Web Application Proxy/Azure AD Application Proxy**</span><span class="sxs-lookup"><span data-stu-id="85ce4-110">**Web Application Proxy/Azure AD Application Proxy**</span></span>|
|:-----|:-----|
|<span data-ttu-id="85ce4-111">Selective HTTP publishing for browser apps</span><span class="sxs-lookup"><span data-stu-id="85ce4-111">Selective HTTP publishing for browser apps</span></span>|<span data-ttu-id="85ce4-112">Available in Web Application Proxy in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="85ce4-112">Available in Web Application Proxy in Windows Server 2012 R2.</span></span> <span data-ttu-id="85ce4-113">Available in Azure AD Application Proxy today.</span><span class="sxs-lookup"><span data-stu-id="85ce4-113">Available in Azure AD Application Proxy today.</span></span>|
|<span data-ttu-id="85ce4-114">Active Directory Federation Services (AD FS) integration</span><span class="sxs-lookup"><span data-stu-id="85ce4-114">Active Directory Federation Services (AD FS) integration</span></span>|<span data-ttu-id="85ce4-115">Available in Web Application Proxy in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="85ce4-115">Available in Web Application Proxy in Windows Server 2012 R2.</span></span> <span data-ttu-id="85ce4-116">Available in Azure AD Application Proxy today.</span><span class="sxs-lookup"><span data-stu-id="85ce4-116">Available in Azure AD Application Proxy today.</span></span>|
|<span data-ttu-id="85ce4-117">Rich protocols publishing (for example, Citrix, Lync, RDG)</span><span class="sxs-lookup"><span data-stu-id="85ce4-117">Rich protocols publishing (for example, Citrix, Lync, RDG)</span></span>|<span data-ttu-id="85ce4-118">Available in Web Application Proxy in Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="85ce4-118">Available in Web Application Proxy in Windows Server 2012 R2.</span></span> <span data-ttu-id="85ce4-119">Available in Azure AD Application Proxy today.</span><span class="sxs-lookup"><span data-stu-id="85ce4-119">Available in Azure AD Application Proxy today.</span></span>|
|<span data-ttu-id="85ce4-120">Preauthentication for ActiveSync (HTTP Basic) and RDG</span><span class="sxs-lookup"><span data-stu-id="85ce4-120">Preauthentication for ActiveSync (HTTP Basic) and RDG</span></span>|<span data-ttu-id="85ce4-121">Currently not available in Web Application Proxy or Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="85ce4-121">Currently not available in Web Application Proxy or Azure AD Application Proxy.</span></span>|
|<span data-ttu-id="85ce4-122">Portal</span><span class="sxs-lookup"><span data-stu-id="85ce4-122">Portal</span></span>|<span data-ttu-id="85ce4-123">Use Intune or System Center for Web Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="85ce4-123">Use Intune or System Center for Web Application Proxy.</span></span> <span data-ttu-id="85ce4-124">Use Azure AD Access Panel or Office 365 App Launcher for Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="85ce4-124">Use Azure AD Access Panel or Office 365 App Launcher for Azure AD Application Proxy.</span></span>|
|<span data-ttu-id="85ce4-125">Endpoint health detection</span><span class="sxs-lookup"><span data-stu-id="85ce4-125">Endpoint health detection</span></span>|<span data-ttu-id="85ce4-126">Use Intune or System Center.</span><span class="sxs-lookup"><span data-stu-id="85ce4-126">Use Intune or System Center.</span></span>|
|<span data-ttu-id="85ce4-127">SSL tunneling</span><span class="sxs-lookup"><span data-stu-id="85ce4-127">SSL tunneling</span></span>|<span data-ttu-id="85ce4-128">Use Windows SSL or VPN capability.</span><span class="sxs-lookup"><span data-stu-id="85ce4-128">Use Windows SSL or VPN capability.</span></span>|
|<span data-ttu-id="85ce4-129">Layer 2/3 firewall</span><span class="sxs-lookup"><span data-stu-id="85ce4-129">Layer 2/3 firewall</span></span>|<span data-ttu-id="85ce4-130">Use Windows Server capabilities.</span><span class="sxs-lookup"><span data-stu-id="85ce4-130">Use Windows Server capabilities.</span></span>|
|<span data-ttu-id="85ce4-131">Web application firewall</span><span class="sxs-lookup"><span data-stu-id="85ce4-131">Web application firewall</span></span>|<span data-ttu-id="85ce4-132">No current solution from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="85ce4-132">No current solution from Microsoft.</span></span>|
|<span data-ttu-id="85ce4-133">Secure web gateway (forward proxy)</span><span class="sxs-lookup"><span data-stu-id="85ce4-133">Secure web gateway (forward proxy)</span></span>|<span data-ttu-id="85ce4-134">No current solution from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="85ce4-134">No current solution from Microsoft.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="85ce4-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="85ce4-135">Next steps</span></span>

[<span data-ttu-id="85ce4-136">Blog: Web Application Proxy</span><span class="sxs-lookup"><span data-stu-id="85ce4-136">Blog: Web Application Proxy</span></span>](https://blogs.technet.microsoft.com/applicationproxyblog/tag/web-application-proxy)<br>
[<span data-ttu-id="85ce4-137">Blog: Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="85ce4-137">Blog: Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/applicationproxyblog/tag/aad-ap)
