---
title: Application and service availability issues for Microsoft Azure Cloud Services FAQ| Microsoft Docs
description: This article lists the frequently asked questions about application and service availability for Microsoft Azure Cloud Services.
services: cloud-services
documentationcenter: ''
author: genlin
manager: cshepard
editor: ''
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2018
ms.author: genli
ms.openlocfilehash: 5b64aface74afad9e6641992c3cfbe3f531696c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868729"
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="27270-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span><span class="sxs-lookup"><span data-stu-id="27270-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="27270-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span><span class="sxs-lookup"><span data-stu-id="27270-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="27270-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span><span class="sxs-lookup"><span data-stu-id="27270-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="27270-106">My role got recycled.</span><span class="sxs-lookup"><span data-stu-id="27270-106">My role got recycled.</span></span> <span data-ttu-id="27270-107">Was there any update rolled out for my cloud service?</span><span class="sxs-lookup"><span data-stu-id="27270-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="27270-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span><span class="sxs-lookup"><span data-stu-id="27270-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="27270-109"> The Guest OS is only one such update in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="27270-109"> The Guest OS is only one such update in the pipeline.</span></span> <span data-ttu-id="27270-110">A release can be affected by many other factors.</span><span class="sxs-lookup"><span data-stu-id="27270-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="27270-111">In addition, Azure runs on hundreds of thousands of machines.</span><span class="sxs-lookup"><span data-stu-id="27270-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="27270-112">Therefore, it's impossible to predict the exact date and time when your roles will reboot.</span><span class="sxs-lookup"><span data-stu-id="27270-112">Therefore, it's impossible to predict the exact date and time when your roles will reboot.</span></span> <span data-ttu-id="27270-113">We update the Guest OS Update RSS Feed with the latest information that we have, but you should consider that reported time to be an approximate value.</span><span class="sxs-lookup"><span data-stu-id="27270-113">We update the Guest OS Update RSS Feed with the latest information that we have, but you should consider that reported time to be an approximate value.</span></span> <span data-ttu-id="27270-114">We are aware that this is problematic for customers and are working on a plan to limit or precisely time reboots.</span><span class="sxs-lookup"><span data-stu-id="27270-114">We are aware that this is problematic for customers and are working on a plan to limit or precisely time reboots.</span></span>

<span data-ttu-id="27270-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="27270-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="27270-116">For helpful information on restarts and pointers to technical details of Guest and Host OS updates, see the MSDN blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span><span class="sxs-lookup"><span data-stu-id="27270-116">For helpful information on restarts and pointers to technical details of Guest and Host OS updates, see the MSDN blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-the-first-request-to-my-cloud-service-after-the-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="27270-117">Why does the first request to my cloud service after the service has been idle for some time take longer than usual?</span><span class="sxs-lookup"><span data-stu-id="27270-117">Why does the first request to my cloud service after the service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="27270-118">When the Web Server receives the first request, it first recompiles the code and then processes the request.</span><span class="sxs-lookup"><span data-stu-id="27270-118">When the Web Server receives the first request, it first recompiles the code and then processes the request.</span></span> <span data-ttu-id="27270-119">That's why the first request takes longer than the others.</span><span class="sxs-lookup"><span data-stu-id="27270-119">That's why the first request takes longer than the others.</span></span> <span data-ttu-id="27270-120">By default, the app pool gets shut down in cases of user inactivity.</span><span class="sxs-lookup"><span data-stu-id="27270-120">By default, the app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="27270-121">The app pool will also recycle by default every 1,740 minutes (29 hours).</span><span class="sxs-lookup"><span data-stu-id="27270-121">The app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="27270-122">Internet Information Services (IIS) application pools can be periodically recycled to avoid unstable states that can lead to application crashes, hangs, or memory leaks.</span><span class="sxs-lookup"><span data-stu-id="27270-122">Internet Information Services (IIS) application pools can be periodically recycled to avoid unstable states that can lead to application crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="27270-123">The following documents will help you understand and mitigate this issue:</span><span class="sxs-lookup"><span data-stu-id="27270-123">The following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="27270-124">Fixing slow initial load for IIS</span><span class="sxs-lookup"><span data-stu-id="27270-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="27270-125">IIS 7.5 web application first request after app-pool recycle very slow</span><span class="sxs-lookup"><span data-stu-id="27270-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="27270-126">If you want to change the default behavior of IIS, you will need to use startup tasks, because if you manually apply changes to the Web Role instances, the changes will eventually be lost.</span><span class="sxs-lookup"><span data-stu-id="27270-126">If you want to change the default behavior of IIS, you will need to use startup tasks, because if you manually apply changes to the Web Role instances, the changes will eventually be lost.</span></span>

<span data-ttu-id="27270-127">For more information, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="27270-127">For more information, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
