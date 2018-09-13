---
title: Pen Testing | Microsoft Docs
description: The article provides an overview of the penetration testing (pentest) process and how perform pentest against your apps running in Azure infrastructure.
services: security
documentationcenter: na
author: TerryLanfear
manager: mbaldwin
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/13/2018
ms.author: barclayn
ms.openlocfilehash: 4096cf3a44b7c32ed94fdd2ef5dcbad9db08a386
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811732"
---
# <a name="pen-testing"></a><span data-ttu-id="55779-103">Pen Testing</span><span class="sxs-lookup"><span data-stu-id="55779-103">Pen Testing</span></span>
<span data-ttu-id="55779-104">One of the benefits of using Azure for application testing and deployment is that you can quickly get environments created.</span><span class="sxs-lookup"><span data-stu-id="55779-104">One of the benefits of using Azure for application testing and deployment is that you can quickly get environments created.</span></span>  <span data-ttu-id="55779-105">You don’t have to worry about requisitioning, acquiring, and “racking and stacking” your own on-premises hardware.</span><span class="sxs-lookup"><span data-stu-id="55779-105">You don’t have to worry about requisitioning, acquiring, and “racking and stacking” your own on-premises hardware.</span></span>

<span data-ttu-id="55779-106">This is great – but you still need to make sure you perform your normal security due diligence.</span><span class="sxs-lookup"><span data-stu-id="55779-106">This is great – but you still need to make sure you perform your normal security due diligence.</span></span> <span data-ttu-id="55779-107">One of the things you need to do is penetration test the applications you deploy in Azure.</span><span class="sxs-lookup"><span data-stu-id="55779-107">One of the things you need to do is penetration test the applications you deploy in Azure.</span></span>

<span data-ttu-id="55779-108">You might already know that Microsoft performs [penetration testing of our Azure environment](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e).</span><span class="sxs-lookup"><span data-stu-id="55779-108">You might already know that Microsoft performs [penetration testing of our Azure environment](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e).</span></span> <span data-ttu-id="55779-109">This helps drive Azure improvements.</span><span class="sxs-lookup"><span data-stu-id="55779-109">This helps drive Azure improvements.</span></span>

<span data-ttu-id="55779-110">We don’t pen test your application for you, but we do understand that you will want and need to perform pen testing on your own applications.</span><span class="sxs-lookup"><span data-stu-id="55779-110">We don’t pen test your application for you, but we do understand that you will want and need to perform pen testing on your own applications.</span></span> <span data-ttu-id="55779-111">That’s a good thing, because when you enhance the security of your applications, you help make the entire Azure ecosystem more secure.</span><span class="sxs-lookup"><span data-stu-id="55779-111">That’s a good thing, because when you enhance the security of your applications, you help make the entire Azure ecosystem more secure.</span></span>

<span data-ttu-id="55779-112">What to do?</span><span class="sxs-lookup"><span data-stu-id="55779-112">What to do?</span></span>

<span data-ttu-id="55779-113">As of June 15, 2017, Microsoft no longer requires pre-approval to conduct a penetration tests against Azure resources.</span><span class="sxs-lookup"><span data-stu-id="55779-113">As of June 15, 2017, Microsoft no longer requires pre-approval to conduct a penetration tests against Azure resources.</span></span> <span data-ttu-id="55779-114">Customers who wish to formally document upcoming penetration testing engagements against Microsoft Azure are encouraged to fill out the [Azure Service Penetration Testing Notification form](https://portal.msrc.microsoft.com/en-us/engage/pentest).</span><span class="sxs-lookup"><span data-stu-id="55779-114">Customers who wish to formally document upcoming penetration testing engagements against Microsoft Azure are encouraged to fill out the [Azure Service Penetration Testing Notification form](https://portal.msrc.microsoft.com/en-us/engage/pentest).</span></span> <span data-ttu-id="55779-115">This process is only related to Microsoft Azure, and not applicable to any other Microsoft Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="55779-115">This process is only related to Microsoft Azure, and not applicable to any other Microsoft Cloud Service.</span></span>

>[!IMPORTANT]
><span data-ttu-id="55779-116">While notifying Microsoft of pen testing activities is no longer required customers must still comply with the [Microsoft Cloud Unified Penetration Testing Rules of Engagement](https://technet.microsoft.com/mt784683).</span><span class="sxs-lookup"><span data-stu-id="55779-116">While notifying Microsoft of pen testing activities is no longer required customers must still comply with the [Microsoft Cloud Unified Penetration Testing Rules of Engagement](https://technet.microsoft.com/mt784683).</span></span>

<span data-ttu-id="55779-117">Standard tests you can perform include:</span><span class="sxs-lookup"><span data-stu-id="55779-117">Standard tests you can perform include:</span></span>

* <span data-ttu-id="55779-118">Tests on your endpoints to uncover the [Open Web Application Security Project (OWASP) top 10 vulnerabilities](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span><span class="sxs-lookup"><span data-stu-id="55779-118">Tests on your endpoints to uncover the [Open Web Application Security Project (OWASP) top 10 vulnerabilities](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span></span>
* <span data-ttu-id="55779-119">[Fuzz testing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) of your endpoints</span><span class="sxs-lookup"><span data-stu-id="55779-119">[Fuzz testing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) of your endpoints</span></span>
* <span data-ttu-id="55779-120">[Port scanning](https://en.wikipedia.org/wiki/Port_scanner) of your endpoints</span><span class="sxs-lookup"><span data-stu-id="55779-120">[Port scanning](https://en.wikipedia.org/wiki/Port_scanner) of your endpoints</span></span>

<span data-ttu-id="55779-121">One type of test that you can’t perform is any kind of [Denial of Service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) attack.</span><span class="sxs-lookup"><span data-stu-id="55779-121">One type of test that you can’t perform is any kind of [Denial of Service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) attack.</span></span> <span data-ttu-id="55779-122">This includes initiating a DoS attack itself, or performing related tests that might determine, demonstrate or simulate any type of DoS attack.</span><span class="sxs-lookup"><span data-stu-id="55779-122">This includes initiating a DoS attack itself, or performing related tests that might determine, demonstrate or simulate any type of DoS attack.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55779-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="55779-123">Next steps</span></span>

- <span data-ttu-id="55779-124">Are you ready to get started with pen testing your applications hosted in Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="55779-124">Are you ready to get started with pen testing your applications hosted in Microsoft Azure?</span></span> <span data-ttu-id="55779-125">If so, then head on over to the [Penetration Testing Rules of Engagement](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=2) and fill out the testing notification form.</span><span class="sxs-lookup"><span data-stu-id="55779-125">If so, then head on over to the [Penetration Testing Rules of Engagement](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=2) and fill out the testing notification form.</span></span>
