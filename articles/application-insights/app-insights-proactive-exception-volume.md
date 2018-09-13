---
title: Smart Detection - Abnormal rise in exception volume, in Azure Application Insights | Microsoft Docs
description: Monitor application exceptions with Azure Application Insights for unusual patterns in exception volume.
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
ms.date: 12/08/2017
ms.author: mbullwin
ms.openlocfilehash: 898cc0935051f65cb0f2977c7d90e998ec32cdd3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857993"
---
# <a name="abnormal-rise-in-exception-volume-preview"></a><span data-ttu-id="ee04d-103">Abnormal rise in exception volume (preview)</span><span class="sxs-lookup"><span data-stu-id="ee04d-103">Abnormal rise in exception volume (preview)</span></span>

<span data-ttu-id="ee04d-104">Application Insights automatically analyzes the exceptions thrown in your application, and can warn you about unusual patterns in your exception telemetry.</span><span class="sxs-lookup"><span data-stu-id="ee04d-104">Application Insights automatically analyzes the exceptions thrown in your application, and can warn you about unusual patterns in your exception telemetry.</span></span>

<span data-ttu-id="ee04d-105">This feature requires no special setup, other than [configuring exception reporting](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net-exceptions#set-up-exception-reporting) for your app.</span><span class="sxs-lookup"><span data-stu-id="ee04d-105">This feature requires no special setup, other than [configuring exception reporting](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net-exceptions#set-up-exception-reporting) for your app.</span></span> <span data-ttu-id="ee04d-106">It is active when your app generates enough exception telemetry.</span><span class="sxs-lookup"><span data-stu-id="ee04d-106">It is active when your app generates enough exception telemetry.</span></span>

## <a name="when-would-i-get-this-type-of-smart-detection-notification"></a><span data-ttu-id="ee04d-107">When would I get this type of smart detection notification?</span><span class="sxs-lookup"><span data-stu-id="ee04d-107">When would I get this type of smart detection notification?</span></span>
<span data-ttu-id="ee04d-108">You might get this type of notification if your app is exhibiting an abnormal rise in the number of exceptions of a specific type during a day, compared to a baseline calculated over the previous seven days.</span><span class="sxs-lookup"><span data-stu-id="ee04d-108">You might get this type of notification if your app is exhibiting an abnormal rise in the number of exceptions of a specific type during a day, compared to a baseline calculated over the previous seven days.</span></span>
<span data-ttu-id="ee04d-109">Machine learning algorithms are being used for detecting the rise in exception count, while taking into account a natural growth in your application usage.</span><span class="sxs-lookup"><span data-stu-id="ee04d-109">Machine learning algorithms are being used for detecting the rise in exception count, while taking into account a natural growth in your application usage.</span></span>

## <a name="does-my-app-definitely-have-a-problem"></a><span data-ttu-id="ee04d-110">Does my app definitely have a problem?</span><span class="sxs-lookup"><span data-stu-id="ee04d-110">Does my app definitely have a problem?</span></span>
<span data-ttu-id="ee04d-111">No, a notification doesn't mean that your app definitely has a problem.</span><span class="sxs-lookup"><span data-stu-id="ee04d-111">No, a notification doesn't mean that your app definitely has a problem.</span></span> <span data-ttu-id="ee04d-112">Although an excessive number of exceptions usually indicates an application issue, these exceptions might be benign and handled correctly by your application.</span><span class="sxs-lookup"><span data-stu-id="ee04d-112">Although an excessive number of exceptions usually indicates an application issue, these exceptions might be benign and handled correctly by your application.</span></span>

## <a name="how-do-i-fix-it"></a><span data-ttu-id="ee04d-113">How do I fix it?</span><span class="sxs-lookup"><span data-stu-id="ee04d-113">How do I fix it?</span></span>
<span data-ttu-id="ee04d-114">The notifications include diagnostic information to support in the diagnostics process:</span><span class="sxs-lookup"><span data-stu-id="ee04d-114">The notifications include diagnostic information to support in the diagnostics process:</span></span>
1. <span data-ttu-id="ee04d-115">**Triage.**</span><span class="sxs-lookup"><span data-stu-id="ee04d-115">**Triage.**</span></span> <span data-ttu-id="ee04d-116">The notification shows you how many users or how many requests are affected.</span><span class="sxs-lookup"><span data-stu-id="ee04d-116">The notification shows you how many users or how many requests are affected.</span></span> <span data-ttu-id="ee04d-117">This can help you assign a priority to the problem.</span><span class="sxs-lookup"><span data-stu-id="ee04d-117">This can help you assign a priority to the problem.</span></span>
2. <span data-ttu-id="ee04d-118">**Scope.**</span><span class="sxs-lookup"><span data-stu-id="ee04d-118">**Scope.**</span></span> <span data-ttu-id="ee04d-119">Is the problem affecting all traffic, or just some operation?</span><span class="sxs-lookup"><span data-stu-id="ee04d-119">Is the problem affecting all traffic, or just some operation?</span></span> <span data-ttu-id="ee04d-120">This information can be obtained from the notification.</span><span class="sxs-lookup"><span data-stu-id="ee04d-120">This information can be obtained from the notification.</span></span>
3. <span data-ttu-id="ee04d-121">**Diagnose.**</span><span class="sxs-lookup"><span data-stu-id="ee04d-121">**Diagnose.**</span></span> <span data-ttu-id="ee04d-122">The detection contains information about the method from which the exception was thrown, as well as the exception type.</span><span class="sxs-lookup"><span data-stu-id="ee04d-122">The detection contains information about the method from which the exception was thrown, as well as the exception type.</span></span> <span data-ttu-id="ee04d-123">You can also use the related items and reports linking to supporting information, to help you further diagnose the issue.</span><span class="sxs-lookup"><span data-stu-id="ee04d-123">You can also use the related items and reports linking to supporting information, to help you further diagnose the issue.</span></span>