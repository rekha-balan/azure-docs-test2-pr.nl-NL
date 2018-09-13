---
title: List of Azure Diagnostics configuration schema versions | Microsoft Docs
description: Used to configure the collection of perf counters in Azure Virtual Machines, VM Scale Sets, Service Fabric, and Cloud Services.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/09/2017
ms.author: robb
ms.openlocfilehash: 5d0894430dc915fc46d753a0b672de3b51ce3888
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555073"
---
# <a name="list-of-azure-diagnostics-versions"></a><span data-ttu-id="48151-103">List of Azure Diagnostics Versions</span><span class="sxs-lookup"><span data-stu-id="48151-103">List of Azure Diagnostics Versions</span></span>
<span data-ttu-id="48151-104">This page indexes Azure Diagnostics Schema versions shipped as part of the Microsoft Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="48151-104">This page indexes Azure Diagnostics Schema versions shipped as part of the Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="48151-105">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="48151-105">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="48151-106">This page is only relevant if you are using one of these services.</span><span class="sxs-lookup"><span data-stu-id="48151-106">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="48151-107">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="48151-107">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="48151-108">Azure SDK and Diagnostics versions shipping chart</span><span class="sxs-lookup"><span data-stu-id="48151-108">Azure SDK and Diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="48151-109">Azure SDK version</span><span class="sxs-lookup"><span data-stu-id="48151-109">Azure SDK version</span></span> | <span data-ttu-id="48151-110">Azure Diagnostics version</span><span class="sxs-lookup"><span data-stu-id="48151-110">Azure Diagnostics version</span></span> | <span data-ttu-id="48151-111">Model</span><span class="sxs-lookup"><span data-stu-id="48151-111">Model</span></span>|  
|------------------|---------------------------|------|  
|<span data-ttu-id="48151-112">1.x</span><span class="sxs-lookup"><span data-stu-id="48151-112">1.x</span></span>               |<span data-ttu-id="48151-113">1.0</span><span class="sxs-lookup"><span data-stu-id="48151-113">1.0</span></span>                         | <span data-ttu-id="48151-114">plug-in</span><span class="sxs-lookup"><span data-stu-id="48151-114">plug-in</span></span>|  
|<span data-ttu-id="48151-115">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="48151-115">2.0 - 2.4</span></span>         |<span data-ttu-id="48151-116">1.0</span><span class="sxs-lookup"><span data-stu-id="48151-116">1.0</span></span>                         |<span data-ttu-id="48151-117">"</span><span class="sxs-lookup"><span data-stu-id="48151-117">"</span></span>|  
|<span data-ttu-id="48151-118">2.5</span><span class="sxs-lookup"><span data-stu-id="48151-118">2.5</span></span>               |<span data-ttu-id="48151-119">1.2</span><span class="sxs-lookup"><span data-stu-id="48151-119">1.2</span></span>                         |<span data-ttu-id="48151-120">extension</span><span class="sxs-lookup"><span data-stu-id="48151-120">extension</span></span>|  
|<span data-ttu-id="48151-121">2.6</span><span class="sxs-lookup"><span data-stu-id="48151-121">2.6</span></span>               |<span data-ttu-id="48151-122">1.3</span><span class="sxs-lookup"><span data-stu-id="48151-122">1.3</span></span>                         |<span data-ttu-id="48151-123">"</span><span class="sxs-lookup"><span data-stu-id="48151-123">"</span></span>|  
|<span data-ttu-id="48151-124">2.7</span><span class="sxs-lookup"><span data-stu-id="48151-124">2.7</span></span>               |<span data-ttu-id="48151-125">1.4</span><span class="sxs-lookup"><span data-stu-id="48151-125">1.4</span></span>                         |<span data-ttu-id="48151-126">"</span><span class="sxs-lookup"><span data-stu-id="48151-126">"</span></span>|  
|<span data-ttu-id="48151-127">2.8</span><span class="sxs-lookup"><span data-stu-id="48151-127">2.8</span></span>               |<span data-ttu-id="48151-128">1.5</span><span class="sxs-lookup"><span data-stu-id="48151-128">1.5</span></span>                         |<span data-ttu-id="48151-129">"</span><span class="sxs-lookup"><span data-stu-id="48151-129">"</span></span>|  
|<span data-ttu-id="48151-130">2.9</span><span class="sxs-lookup"><span data-stu-id="48151-130">2.9</span></span>               |<span data-ttu-id="48151-131">1.6</span><span class="sxs-lookup"><span data-stu-id="48151-131">1.6</span></span>                         |<span data-ttu-id="48151-132">"</span><span class="sxs-lookup"><span data-stu-id="48151-132">"</span></span>|
|<span data-ttu-id="48151-133">2.96</span><span class="sxs-lookup"><span data-stu-id="48151-133">2.96</span></span>              |<span data-ttu-id="48151-134">1.7</span><span class="sxs-lookup"><span data-stu-id="48151-134">1.7</span></span>                         |<span data-ttu-id="48151-135">"</span><span class="sxs-lookup"><span data-stu-id="48151-135">"</span></span>|



 <span data-ttu-id="48151-136">Azure Diagnostics version 1.0 first shipped in a plug-in model, meaning that when you installed the Azure SDK, you got the version of Azure diagnostics shipped with it.</span><span class="sxs-lookup"><span data-stu-id="48151-136">Azure Diagnostics version 1.0 first shipped in a plug-in model, meaning that when you installed the Azure SDK, you got the version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="48151-137">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went to an extension model.</span><span class="sxs-lookup"><span data-stu-id="48151-137">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went to an extension model.</span></span> <span data-ttu-id="48151-138">The tools to utilize new features were only available in newer Azure SDKs, but any Cloud Service or Virtual Machine using diagnostics would pick up the latest shipping version directly from Azure.</span><span class="sxs-lookup"><span data-stu-id="48151-138">The tools to utilize new features were only available in newer Azure SDKs, but any Cloud Service or Virtual Machine using diagnostics would pick up the latest shipping version directly from Azure.</span></span>  

 <span data-ttu-id="48151-139">For example, anyone still using SDK 2.5 would be loading Diagnostics 1.5, whether or not they were using the newer features.</span><span class="sxs-lookup"><span data-stu-id="48151-139">For example, anyone still using SDK 2.5 would be loading Diagnostics 1.5, whether or not they were using the newer features.</span></span>  

## <a name="azure-diagnostics-schemas-index"></a><span data-ttu-id="48151-140">Azure Diagnostics schemas index</span><span class="sxs-lookup"><span data-stu-id="48151-140">Azure Diagnostics schemas index</span></span>  
[<span data-ttu-id="48151-141">Diagnostics 1.0 Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="48151-141">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="48151-142">Diagnostics 1.2 Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="48151-142">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="48151-143">Diagnostics 1.3 and later Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="48151-143">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  
