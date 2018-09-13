---
title: Smart Detection - Potential Memory Leak detected by Azure Application Insights | Microsoft Docs
description: Monitor applications with Azure Application Insights for potential memory leaks.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 12/12/2017
ms.author: mbullwin
ms.openlocfilehash: 25d26db3cd11fff7f7e9ba472247a920ecddea33
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966775"
---
# <a name="memory-leak-detection-preview"></a><span data-ttu-id="50bf3-103">Memory leak detection (preview)</span><span class="sxs-lookup"><span data-stu-id="50bf3-103">Memory leak detection (preview)</span></span>

<span data-ttu-id="50bf3-104">Application Insights automatically analyzes the memory consumption of each process in your application, and can warn you about potential memory leaks or increased memory consumption.</span><span class="sxs-lookup"><span data-stu-id="50bf3-104">Application Insights automatically analyzes the memory consumption of each process in your application, and can warn you about potential memory leaks or increased memory consumption.</span></span>

<span data-ttu-id="50bf3-105">This feature requires no special setup, other than [configuring performance counters](https://docs.microsoft.com/azure/application-insights/app-insights-performance-counters) for your app.</span><span class="sxs-lookup"><span data-stu-id="50bf3-105">This feature requires no special setup, other than [configuring performance counters](https://docs.microsoft.com/azure/application-insights/app-insights-performance-counters) for your app.</span></span> <span data-ttu-id="50bf3-106">It's active when your app generates enough memory performance counters telemetry (for example, Private Bytes).</span><span class="sxs-lookup"><span data-stu-id="50bf3-106">It's active when your app generates enough memory performance counters telemetry (for example, Private Bytes).</span></span>

## <a name="when-would-i-get-this-type-of-smart-detection-notification"></a><span data-ttu-id="50bf3-107">When would I get this type of smart detection notification?</span><span class="sxs-lookup"><span data-stu-id="50bf3-107">When would I get this type of smart detection notification?</span></span>
<span data-ttu-id="50bf3-108">A typical notification will follow a consistent increase in memory consumption over a long period of time, in one or more processes and/or one or more machines, which are part of your application.</span><span class="sxs-lookup"><span data-stu-id="50bf3-108">A typical notification will follow a consistent increase in memory consumption over a long period of time, in one or more processes and/or one or more machines, which are part of your application.</span></span> <span data-ttu-id="50bf3-109">Machine learning algorithms are used for detecting increased memory consumption that matches the pattern of a memory leak.</span><span class="sxs-lookup"><span data-stu-id="50bf3-109">Machine learning algorithms are used for detecting increased memory consumption that matches the pattern of a memory leak.</span></span>

## <a name="does-my-app-really-have-a-problem"></a><span data-ttu-id="50bf3-110">Does my app really have a problem?</span><span class="sxs-lookup"><span data-stu-id="50bf3-110">Does my app really have a problem?</span></span>
<span data-ttu-id="50bf3-111">No, a notification doesn't mean that your app definitely has a problem.</span><span class="sxs-lookup"><span data-stu-id="50bf3-111">No, a notification doesn't mean that your app definitely has a problem.</span></span> <span data-ttu-id="50bf3-112">Although memory leak patterns usually indicate an application issue, these patterns could be typical to your specific process, or could have a natural business justification, and can be ignored.</span><span class="sxs-lookup"><span data-stu-id="50bf3-112">Although memory leak patterns usually indicate an application issue, these patterns could be typical to your specific process, or could have a natural business justification, and can be ignored.</span></span>

## <a name="how-do-i-fix-it"></a><span data-ttu-id="50bf3-113">How do I fix it?</span><span class="sxs-lookup"><span data-stu-id="50bf3-113">How do I fix it?</span></span>
<span data-ttu-id="50bf3-114">The notifications include diagnostic information to support in the diagnostic analysis process:</span><span class="sxs-lookup"><span data-stu-id="50bf3-114">The notifications include diagnostic information to support in the diagnostic analysis process:</span></span>
1. <span data-ttu-id="50bf3-115">**Triage.**</span><span class="sxs-lookup"><span data-stu-id="50bf3-115">**Triage.**</span></span> <span data-ttu-id="50bf3-116">The notification shows you the amount of memory increase (in GB), and the time range in which the memory has increased.</span><span class="sxs-lookup"><span data-stu-id="50bf3-116">The notification shows you the amount of memory increase (in GB), and the time range in which the memory has increased.</span></span> <span data-ttu-id="50bf3-117">This can help you assign a priority to the problem.</span><span class="sxs-lookup"><span data-stu-id="50bf3-117">This can help you assign a priority to the problem.</span></span>
2. <span data-ttu-id="50bf3-118">**Scope.**</span><span class="sxs-lookup"><span data-stu-id="50bf3-118">**Scope.**</span></span> <span data-ttu-id="50bf3-119">How many machines exhibited the memory leak pattern?</span><span class="sxs-lookup"><span data-stu-id="50bf3-119">How many machines exhibited the memory leak pattern?</span></span> <span data-ttu-id="50bf3-120">How many exceptions were triggered during the potential memory leak?</span><span class="sxs-lookup"><span data-stu-id="50bf3-120">How many exceptions were triggered during the potential memory leak?</span></span> <span data-ttu-id="50bf3-121">This information can be obtained from the notification.</span><span class="sxs-lookup"><span data-stu-id="50bf3-121">This information can be obtained from the notification.</span></span>
3. <span data-ttu-id="50bf3-122">**Diagnose.**</span><span class="sxs-lookup"><span data-stu-id="50bf3-122">**Diagnose.**</span></span> <span data-ttu-id="50bf3-123">The detection contains the memory leak pattern, showing memory consumption of the process over time.</span><span class="sxs-lookup"><span data-stu-id="50bf3-123">The detection contains the memory leak pattern, showing memory consumption of the process over time.</span></span> <span data-ttu-id="50bf3-124">You can also use the related items and reports linking to supporting information, to help you further diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="50bf3-124">You can also use the related items and reports linking to supporting information, to help you further diagnose the issue.</span></span>
