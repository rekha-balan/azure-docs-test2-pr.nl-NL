---
title: Real-time event processing with Stream Analytics event processing | Microsoft Docs
description: Learn how a set of Azure services can interoperate for enabling real-time event processing and analytics.
keywords: real-time processing, event processing, reference architecture
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: ''
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: 23a8e5e2c9162f1268a8968bcc87e2ffdf50fe37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563452"
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="483f9-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="483f9-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="483f9-105">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="483f9-105">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="483f9-106">Summary</span><span class="sxs-lookup"><span data-stu-id="483f9-106">Summary</span></span>
<span data-ttu-id="483f9-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span><span class="sxs-lookup"><span data-stu-id="483f9-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span></span> <span data-ttu-id="483f9-108">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span><span class="sxs-lookup"><span data-stu-id="483f9-108">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span></span> <span data-ttu-id="483f9-109">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span><span class="sxs-lookup"><span data-stu-id="483f9-109">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="483f9-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span><span class="sxs-lookup"><span data-stu-id="483f9-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="483f9-111">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span><span class="sxs-lookup"><span data-stu-id="483f9-111">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span></span> <span data-ttu-id="483f9-112">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span><span class="sxs-lookup"><span data-stu-id="483f9-112">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="483f9-113">It also explains some of the scenarios in which customers can benefit from this type of approach.</span><span class="sxs-lookup"><span data-stu-id="483f9-113">It also explains some of the scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="483f9-114">Contents</span><span class="sxs-lookup"><span data-stu-id="483f9-114">Contents</span></span>
* <span data-ttu-id="483f9-115">Executive Summary</span><span class="sxs-lookup"><span data-stu-id="483f9-115">Executive Summary</span></span>
* <span data-ttu-id="483f9-116">Introduction to Real-Time Analytics</span><span class="sxs-lookup"><span data-stu-id="483f9-116">Introduction to Real-Time Analytics</span></span>
* <span data-ttu-id="483f9-117">Value Proposition of Real-Time Data in Azure</span><span class="sxs-lookup"><span data-stu-id="483f9-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="483f9-118">Common Scenarios for Real-Time Analytics</span><span class="sxs-lookup"><span data-stu-id="483f9-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="483f9-119">Architecture and Components</span><span class="sxs-lookup"><span data-stu-id="483f9-119">Architecture and Components</span></span>
  * <span data-ttu-id="483f9-120">Data Sources</span><span class="sxs-lookup"><span data-stu-id="483f9-120">Data Sources</span></span>
  * <span data-ttu-id="483f9-121">Data-Integration Layer</span><span class="sxs-lookup"><span data-stu-id="483f9-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="483f9-122">Real-time Analytics Layer</span><span class="sxs-lookup"><span data-stu-id="483f9-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="483f9-123">Data Storage Layer</span><span class="sxs-lookup"><span data-stu-id="483f9-123">Data Storage Layer</span></span>
  * <span data-ttu-id="483f9-124">Presentation / Consumption Layer</span><span class="sxs-lookup"><span data-stu-id="483f9-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="483f9-125">Conclusion</span><span class="sxs-lookup"><span data-stu-id="483f9-125">Conclusion</span></span>

<span data-ttu-id="483f9-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="483f9-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="483f9-127">**Published:** January 2015</span><span class="sxs-lookup"><span data-stu-id="483f9-127">**Published:** January 2015</span></span>

<span data-ttu-id="483f9-128">**Revision:** 1.0</span><span class="sxs-lookup"><span data-stu-id="483f9-128">**Revision:** 1.0</span></span>

<span data-ttu-id="483f9-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="483f9-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="483f9-130">Get help</span><span class="sxs-lookup"><span data-stu-id="483f9-130">Get help</span></span>
<span data-ttu-id="483f9-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="483f9-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="483f9-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="483f9-132">Next steps</span></span>
* [<span data-ttu-id="483f9-133">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="483f9-133">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="483f9-134">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="483f9-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="483f9-135">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="483f9-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="483f9-136">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="483f9-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="483f9-137">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="483f9-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

