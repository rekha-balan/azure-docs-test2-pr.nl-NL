---
title: Scheduler High-Availability and Reliability
description: Scheduler High-Availability and Reliability
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: ''
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 7e7fe49de7814b6058468d630f8638720e5864f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775755"
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="89b11-103">Scheduler High-Availability and Reliability</span><span class="sxs-lookup"><span data-stu-id="89b11-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="89b11-104">Azure Scheduler High-Availability</span><span class="sxs-lookup"><span data-stu-id="89b11-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="89b11-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span><span class="sxs-lookup"><span data-stu-id="89b11-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="89b11-106">Geo-redundant service deployment</span><span class="sxs-lookup"><span data-stu-id="89b11-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="89b11-107">Azure Scheduler is available via the UI in almost every geo region that's in Azure today.</span><span class="sxs-lookup"><span data-stu-id="89b11-107">Azure Scheduler is available via the UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="89b11-108">The list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="89b11-108">The list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="89b11-109">If a data center in a hosted region is rendered unavailable, the failover capabilities of Azure Scheduler are such that the service is available from another data center.</span><span class="sxs-lookup"><span data-stu-id="89b11-109">If a data center in a hosted region is rendered unavailable, the failover capabilities of Azure Scheduler are such that the service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="89b11-110">Geo-regional job replication</span><span class="sxs-lookup"><span data-stu-id="89b11-110">Geo-regional job replication</span></span>
<span data-ttu-id="89b11-111">Not only is the Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span><span class="sxs-lookup"><span data-stu-id="89b11-111">Not only is the Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="89b11-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that the job is run from another data center in the paired geographic region.</span><span class="sxs-lookup"><span data-stu-id="89b11-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that the job is run from another data center in the paired geographic region.</span></span>

<span data-ttu-id="89b11-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span><span class="sxs-lookup"><span data-stu-id="89b11-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="89b11-114">When there’s a failure in South Central US, Azure Scheduler ensures that the job is run from North Central US.</span><span class="sxs-lookup"><span data-stu-id="89b11-114">When there’s a failure in South Central US, Azure Scheduler ensures that the job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="89b11-115">As a result, Azure Scheduler ensures that your data stays within the same broader geographic region in case of an Azure failure.</span><span class="sxs-lookup"><span data-stu-id="89b11-115">As a result, Azure Scheduler ensures that your data stays within the same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="89b11-116">As a result, you need not duplicate your job just to add high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span><span class="sxs-lookup"><span data-stu-id="89b11-116">As a result, you need not duplicate your job just to add high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="89b11-117">Azure Scheduler Reliability</span><span class="sxs-lookup"><span data-stu-id="89b11-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="89b11-118">Azure Scheduler guarantees its own high-availability and takes a different approach to user-created jobs.</span><span class="sxs-lookup"><span data-stu-id="89b11-118">Azure Scheduler guarantees its own high-availability and takes a different approach to user-created jobs.</span></span> <span data-ttu-id="89b11-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span><span class="sxs-lookup"><span data-stu-id="89b11-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="89b11-120">Azure Scheduler nonetheless tries to execute your job successfully, by giving you alternative options to deal with failure.</span><span class="sxs-lookup"><span data-stu-id="89b11-120">Azure Scheduler nonetheless tries to execute your job successfully, by giving you alternative options to deal with failure.</span></span> <span data-ttu-id="89b11-121">Azure Scheduler does this in two ways:</span><span class="sxs-lookup"><span data-stu-id="89b11-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="89b11-122">Configurable Retry Policy via “retryPolicy”</span><span class="sxs-lookup"><span data-stu-id="89b11-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="89b11-123">Azure Scheduler allows you to configure a retry policy.</span><span class="sxs-lookup"><span data-stu-id="89b11-123">Azure Scheduler allows you to configure a retry policy.</span></span> <span data-ttu-id="89b11-124">By default, if a job fails, Scheduler tries the job again four more times, at 30-second intervals.</span><span class="sxs-lookup"><span data-stu-id="89b11-124">By default, if a job fails, Scheduler tries the job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="89b11-125">You may re-configure this retry policy to be more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span><span class="sxs-lookup"><span data-stu-id="89b11-125">You may re-configure this retry policy to be more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="89b11-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="89b11-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="89b11-127">If the HTTP endpoint is down for a few hours when your job runs, you may not want to wait one more week for the job to run again since even the default retry policy will fail.</span><span class="sxs-lookup"><span data-stu-id="89b11-127">If the HTTP endpoint is down for a few hours when your job runs, you may not want to wait one more week for the job to run again since even the default retry policy will fail.</span></span> <span data-ttu-id="89b11-128">In such cases, you may reconfigure the standard retry policy to retry every three hours (for example) instead of every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="89b11-128">In such cases, you may reconfigure the standard retry policy to retry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="89b11-129">To learn how to configure a retry policy, refer to [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span><span class="sxs-lookup"><span data-stu-id="89b11-129">To learn how to configure a retry policy, refer to [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="89b11-130">Alternate Endpoint Configurability via “errorAction”</span><span class="sxs-lookup"><span data-stu-id="89b11-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="89b11-131">If the target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back to the alternate error-handling endpoint after following its retry policy.</span><span class="sxs-lookup"><span data-stu-id="89b11-131">If the target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back to the alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="89b11-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span><span class="sxs-lookup"><span data-stu-id="89b11-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="89b11-133">With an alternate endpoint, your own jobs are highly available in the face of failure.</span><span class="sxs-lookup"><span data-stu-id="89b11-133">With an alternate endpoint, your own jobs are highly available in the face of failure.</span></span>

<span data-ttu-id="89b11-134">As an example, in the diagram below, Azure Scheduler follows its retry policy to hit a New York web service.</span><span class="sxs-lookup"><span data-stu-id="89b11-134">As an example, in the diagram below, Azure Scheduler follows its retry policy to hit a New York web service.</span></span> <span data-ttu-id="89b11-135">After the retries fail, it checks if there's an alternate.</span><span class="sxs-lookup"><span data-stu-id="89b11-135">After the retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="89b11-136">It then goes ahead and starts making requests to the alternate with the same retry policy.</span><span class="sxs-lookup"><span data-stu-id="89b11-136">It then goes ahead and starts making requests to the alternate with the same retry policy.</span></span>

![][2]

<span data-ttu-id="89b11-137">Note that the same retry policy applies to both the original action and the alternate error action.</span><span class="sxs-lookup"><span data-stu-id="89b11-137">Note that the same retry policy applies to both the original action and the alternate error action.</span></span> <span data-ttu-id="89b11-138">It’s also possible to have the alternate error action’s action type be different from the main action’s action type.</span><span class="sxs-lookup"><span data-stu-id="89b11-138">It’s also possible to have the alternate error action’s action type be different from the main action’s action type.</span></span> <span data-ttu-id="89b11-139">For example, while the main action may be invoking an HTTP endpoint, the error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span><span class="sxs-lookup"><span data-stu-id="89b11-139">For example, while the main action may be invoking an HTTP endpoint, the error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="89b11-140">To learn how to configure an alternate endpoint, refer to [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span><span class="sxs-lookup"><span data-stu-id="89b11-140">To learn how to configure an alternate endpoint, refer to [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="89b11-141">See Also</span><span class="sxs-lookup"><span data-stu-id="89b11-141">See Also</span></span>
 [<span data-ttu-id="89b11-142">What is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="89b11-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="89b11-143">Azure Scheduler concepts, terminology, and entity hierarchy</span><span class="sxs-lookup"><span data-stu-id="89b11-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="89b11-144">Get started using Scheduler in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="89b11-144">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="89b11-145">Plans and billing in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="89b11-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="89b11-146">How to build complex schedules and advanced recurrence with Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="89b11-146">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="89b11-147">Azure Scheduler REST API reference</span><span class="sxs-lookup"><span data-stu-id="89b11-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="89b11-148">Azure Scheduler PowerShell cmdlets reference</span><span class="sxs-lookup"><span data-stu-id="89b11-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="89b11-149">Azure Scheduler limits, defaults, and error codes</span><span class="sxs-lookup"><span data-stu-id="89b11-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="89b11-150">Azure Scheduler outbound authentication</span><span class="sxs-lookup"><span data-stu-id="89b11-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
