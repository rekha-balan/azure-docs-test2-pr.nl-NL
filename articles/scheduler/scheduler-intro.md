---
title: What is Azure Scheduler? | Microsoft Docs
description: Azure Scheduler allows you to declaratively describe actions to run in the cloud. It then schedules and runs those actions automatically.
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: ''
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a3bf1aacd6978499d7ef77cbcb451a06b857ac38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555479"
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="d266f-105">What is Azure Scheduler?</span><span class="sxs-lookup"><span data-stu-id="d266f-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="d266f-106">Azure Scheduler allows you to declaratively describe actions to run in the cloud.</span><span class="sxs-lookup"><span data-stu-id="d266f-106">Azure Scheduler allows you to declaratively describe actions to run in the cloud.</span></span> <span data-ttu-id="d266f-107">It then schedules and runs those actions automatically.</span><span class="sxs-lookup"><span data-stu-id="d266f-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="d266f-108">Scheduler does this by using [the Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d266f-108">Scheduler does this by using [the Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="d266f-109">Scheduler creates, maintains, and invokes scheduled work.</span><span class="sxs-lookup"><span data-stu-id="d266f-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="d266f-110">Scheduler does not host any workloads or run any code.</span><span class="sxs-lookup"><span data-stu-id="d266f-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="d266f-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span><span class="sxs-lookup"><span data-stu-id="d266f-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="d266f-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span><span class="sxs-lookup"><span data-stu-id="d266f-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="d266f-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads to be run.</span><span class="sxs-lookup"><span data-stu-id="d266f-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads to be run.</span></span> <span data-ttu-id="d266f-114">Azure WebJobs (part of the Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in the background.</span><span class="sxs-lookup"><span data-stu-id="d266f-114">Azure WebJobs (part of the Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in the background.</span></span> <span data-ttu-id="d266f-115">The [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage the communication for these actions.</span><span class="sxs-lookup"><span data-stu-id="d266f-115">The [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage the communication for these actions.</span></span> <span data-ttu-id="d266f-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span><span class="sxs-lookup"><span data-stu-id="d266f-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="d266f-117">There are several scenarios that lend themselves to the usage of Scheduler.</span><span class="sxs-lookup"><span data-stu-id="d266f-117">There are several scenarios that lend themselves to the usage of Scheduler.</span></span> <span data-ttu-id="d266f-118">For example:</span><span class="sxs-lookup"><span data-stu-id="d266f-118">For example:</span></span>

* <span data-ttu-id="d266f-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span><span class="sxs-lookup"><span data-stu-id="d266f-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="d266f-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span><span class="sxs-lookup"><span data-stu-id="d266f-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="d266f-121">For example, an administrator may choose to back up the database at 1:00 A.M.</span><span class="sxs-lookup"><span data-stu-id="d266f-121">For example, an administrator may choose to back up the database at 1:00 A.M.</span></span> <span data-ttu-id="d266f-122">every day for the next nine months.</span><span class="sxs-lookup"><span data-stu-id="d266f-122">every day for the next nine months.</span></span>

<span data-ttu-id="d266f-123">Scheduler allows you to create, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in the portal.</span><span class="sxs-lookup"><span data-stu-id="d266f-123">Scheduler allows you to create, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in the portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="d266f-124">See also</span><span class="sxs-lookup"><span data-stu-id="d266f-124">See also</span></span>
 [<span data-ttu-id="d266f-125">Azure Scheduler concepts, terminology, and entity hierarchy</span><span class="sxs-lookup"><span data-stu-id="d266f-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="d266f-126">Get started using Scheduler in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d266f-126">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="d266f-127">Plans and billing in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="d266f-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="d266f-128">How to build complex schedules and advanced recurrence with Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="d266f-128">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="d266f-129">Azure Scheduler REST API reference</span><span class="sxs-lookup"><span data-stu-id="d266f-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="d266f-130">Azure Scheduler PowerShell cmdlets reference</span><span class="sxs-lookup"><span data-stu-id="d266f-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="d266f-131">Azure Scheduler high-availability and reliability</span><span class="sxs-lookup"><span data-stu-id="d266f-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="d266f-132">Azure Scheduler limits, defaults, and error codes</span><span class="sxs-lookup"><span data-stu-id="d266f-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="d266f-133">Azure Scheduler outbound authentication</span><span class="sxs-lookup"><span data-stu-id="d266f-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

