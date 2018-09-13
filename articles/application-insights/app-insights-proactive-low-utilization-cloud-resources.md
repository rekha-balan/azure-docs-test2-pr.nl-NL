---
title: Smart Detection - Low utilization of cloud resources detected by Azure Application Insights | Microsoft Docs
description: Monitor applications with Azure Application Insights for low utilization of cloud resources.
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
ms.openlocfilehash: ca4f944f605db96a2cedf2682f3ff4c811007ffb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856489"
---
# <a name="low-cpu-utilization-in-cloud-resources-preview"></a><span data-ttu-id="52892-103">Low CPU utilization in cloud resources (preview)</span><span class="sxs-lookup"><span data-stu-id="52892-103">Low CPU utilization in cloud resources (preview)</span></span>

<span data-ttu-id="52892-104">Application Insight automatically analyzes the CPU consumption of each role instance in your application and detects instances with low CPU utilization.</span><span class="sxs-lookup"><span data-stu-id="52892-104">Application Insight automatically analyzes the CPU consumption of each role instance in your application and detects instances with low CPU utilization.</span></span> <span data-ttu-id="52892-105">This detection enables you to decrease your Azure resources and reduce costs, by decreasing the number of role instances each role utilizes, or by decreasing the number of roles.</span><span class="sxs-lookup"><span data-stu-id="52892-105">This detection enables you to decrease your Azure resources and reduce costs, by decreasing the number of role instances each role utilizes, or by decreasing the number of roles.</span></span>

<span data-ttu-id="52892-106">This feature requires no special setup, other than [configuring performance counters](https://docs.microsoft.com/azure/application-insights/app-insights-performance-counters) for your app.</span><span class="sxs-lookup"><span data-stu-id="52892-106">This feature requires no special setup, other than [configuring performance counters](https://docs.microsoft.com/azure/application-insights/app-insights-performance-counters) for your app.</span></span> <span data-ttu-id="52892-107">It's active when your app generates enough CPU performance counter telemetry (% Processor Time).</span><span class="sxs-lookup"><span data-stu-id="52892-107">It's active when your app generates enough CPU performance counter telemetry (% Processor Time).</span></span>

## <a name="when-would-i-get-this-type-of-smart-detection-notification"></a><span data-ttu-id="52892-108">When would I get this type of smart detection notification?</span><span class="sxs-lookup"><span data-stu-id="52892-108">When would I get this type of smart detection notification?</span></span>
<span data-ttu-id="52892-109">A typical notification occurs when many of your Web/Worker Role instances exhibit low CPU utilization.</span><span class="sxs-lookup"><span data-stu-id="52892-109">A typical notification occurs when many of your Web/Worker Role instances exhibit low CPU utilization.</span></span>

## <a name="does-my-app-definitely-consume-too-many-resources"></a><span data-ttu-id="52892-110">Does my app definitely consume too many resources?</span><span class="sxs-lookup"><span data-stu-id="52892-110">Does my app definitely consume too many resources?</span></span>
<span data-ttu-id="52892-111">No, a notification doesn't mean that your app definitely consumes too many resources.</span><span class="sxs-lookup"><span data-stu-id="52892-111">No, a notification doesn't mean that your app definitely consumes too many resources.</span></span> <span data-ttu-id="52892-112">Although such patterns of low CPU utilization usually indicate that resource consumption could be decreased, this behavior could be typical to your specific role, or could have a natural business justification, and can be ignored.</span><span class="sxs-lookup"><span data-stu-id="52892-112">Although such patterns of low CPU utilization usually indicate that resource consumption could be decreased, this behavior could be typical to your specific role, or could have a natural business justification, and can be ignored.</span></span> <span data-ttu-id="52892-113">For example, it could be that multiple instances are needed for other resources, such as memory/network, and not CPU.</span><span class="sxs-lookup"><span data-stu-id="52892-113">For example, it could be that multiple instances are needed for other resources, such as memory/network, and not CPU.</span></span>

## <a name="how-do-i-fix-it"></a><span data-ttu-id="52892-114">How do I fix it?</span><span class="sxs-lookup"><span data-stu-id="52892-114">How do I fix it?</span></span>
<span data-ttu-id="52892-115">The notifications include diagnostic information to support in the diagnostics process:</span><span class="sxs-lookup"><span data-stu-id="52892-115">The notifications include diagnostic information to support in the diagnostics process:</span></span>
1. <span data-ttu-id="52892-116">**Triage.**</span><span class="sxs-lookup"><span data-stu-id="52892-116">**Triage.**</span></span> <span data-ttu-id="52892-117">The notification shows you the roles in your app that exhibit low CPU utilization.</span><span class="sxs-lookup"><span data-stu-id="52892-117">The notification shows you the roles in your app that exhibit low CPU utilization.</span></span> <span data-ttu-id="52892-118">This can help you assign a priority to the problem.</span><span class="sxs-lookup"><span data-stu-id="52892-118">This can help you assign a priority to the problem.</span></span>
2. <span data-ttu-id="52892-119">**Scope.**</span><span class="sxs-lookup"><span data-stu-id="52892-119">**Scope.**</span></span> <span data-ttu-id="52892-120">How many roles exhibited low CPU utilization, and how many instances in each role utilize low CPU?</span><span class="sxs-lookup"><span data-stu-id="52892-120">How many roles exhibited low CPU utilization, and how many instances in each role utilize low CPU?</span></span> <span data-ttu-id="52892-121">This information can be obtained from the notification.</span><span class="sxs-lookup"><span data-stu-id="52892-121">This information can be obtained from the notification.</span></span>
3. <span data-ttu-id="52892-122">**Diagnose.**</span><span class="sxs-lookup"><span data-stu-id="52892-122">**Diagnose.**</span></span> <span data-ttu-id="52892-123">The detection contains the percentage of CPU utilized, showing CPU utilization of each instance over time.</span><span class="sxs-lookup"><span data-stu-id="52892-123">The detection contains the percentage of CPU utilized, showing CPU utilization of each instance over time.</span></span> <span data-ttu-id="52892-124">You can also use the related items and reports linking to supporting information, such as percentiles of CPU utilization, to help you further diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="52892-124">You can also use the related items and reports linking to supporting information, such as percentiles of CPU utilization, to help you further diagnose the issue.</span></span>
